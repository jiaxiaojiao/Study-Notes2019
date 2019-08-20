# Dubbo协议超时实现

Dubbo协议超时实现使用了Future模式，主要涉及类DubboInvoker，ResponseFuture, DefaultFuture。 ResponseFuture.get()在请求还未处理完或未到超时前一直是wait状态；响应达到后，设置请求状态，并进行notify唤醒。

```text
  public Object get() throws RemotingException {
        return get(timeout);
    }

    public Object get(int timeout) throws RemotingException {
        if (timeout <= 0) {
            timeout = Constants.DEFAULT_TIMEOUT;
        }
        if (! isDone()) {
            long start = System.currentTimeMillis();
            lock.lock();
            try {
                while (! isDone()) {
                    done.await(timeout, TimeUnit.MILLISECONDS);
                    if (isDone() || System.currentTimeMillis() - start > timeout) {
                        break;
                    }
                }
            } catch (InterruptedException e) {
                throw new RuntimeException(e);
            } finally {
                lock.unlock();
            }
            if (! isDone()) {
                throw new TimeoutException(sent > 0, channel, getTimeoutMessage(false));
            }
        }
        return returnFromResponse();
    }

    public static void received(Channel channel, Response response) {
        try {
            DefaultFuture future = FUTURES.remove(response.getId());
            if (future != null) {
                future.doReceived(response);
            } else {
                logger.warn("The timeout response finally returned at " 
                            + (new SimpleDateFormat("yyyy-MM-dd HH:mm:ss.SSS").format(new Date())) 
                            + ", response " + response 
                            + (channel == null ? "" : ", channel: " + channel.getLocalAddress() 
                                + " -> " + channel.getRemoteAddress()));
            }
        } finally {
            CHANNELS.remove(response.getId());
        }
    }

    private void doReceived(Response res) {
        lock.lock();
        try {
            response = res;
            if (done != null) {
                done.signal();
            }
        } finally {
            lock.unlock();
        }
        if (callback != null) {
            invokeCallback(callback);
        }
    }
```