## 使用vue-cli初始化vue项目
1. 已经安装完成 Node.js vue npm
2. [vue init](#vue-init)
3. [cd 到项目目录，运行项目](#到项目目录-运行项目)
4. 启动后关闭， CTRL + C 然后有提示。
5. [项目结构](#项目结构)

### vue init
cmd 打开命令行 ，cd到希望创建vue项目的目录。

    ```text
    # 创建一个基于 webpack 模板的新项目
    vue init webpack vue-test-2
    ```
    
    # 这里需要进行一些配置，默认回车即可

    ```text
    ? Project name vue-test-2
    ? Project description test vue project 2
    ? Author v-jiaxiaojiao <v-jiaxiaojiao2019@jd.com>
    ? Vue build standalone
    ? Install vue-router? Yes
    ? Use ESLint to lint your code? Yes
    ? Pick an ESLint preset Standard
    ? Set up unit tests Yes
    ? Pick a test runner jest
    ? Setup e2e tests with Nightwatch? Yes
    ? Should we run `npm install` for you after the project has been created? (recommended) npm
    
       vue-cli · Generated "vue-test-2".
    
    
    # Installing project dependencies ...
    # ========================
    
    npm WARN deprecated extract-text-webpack-plugin@3.0.2: Deprecated. Please use https://github.com/webpack-contrib/mini-css-extract-plugin
    npm WARN deprecated browserslist@2.11.3: Browserslist 2 could fail on reading Browserslist >3.0 config used in other tools.
    npm WARN deprecated json3@3.3.2: Please use the native JSON object instead of JSON 3
    npm WARN deprecated flatten@1.0.2: I wrote this module a very long time ago; you should use something else.
    npm WARN deprecated browserslist@1.7.7: Browserslist 2 could fail on reading Browserslist >3.0 config used in other tools.
    npm WARN deprecated socks@1.1.10: If using 2.x branch, please upgrade to at least 2.1.6 to avoid a serious bug with socket data flow and an import issue introduced in 2.1.0
    npm WARN deprecated circular-json@0.3.3: CircularJSON is in maintenance only, flatted is its successor.
    npm WARN deprecated left-pad@1.3.0: use String.prototype.padStart()
    
    > chromedriver@2.46.0 install E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\chromedriver
    > node install.js
    
    Current existing ChromeDriver binary is unavailable, proceding with download and extraction.
    Downloading from file:  https://chromedriver.storage.googleapis.com/2.46/chromedriver_win32.zip
    Saving to file: C:\Users\ADMINI~1.JRA\AppData\Local\Temp\2.46\chromedriver\chromedriver_win32.zip
    Received 781K...
    Received 1568K...
    Received 2352K...
    Received 3136K...
    Received 3920K...
    Received 4523K total.
    Extracting zip contents
    Copying to target path E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\chromedriver\lib\chromedriver
    Done. ChromeDriver binary available at E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\chromedriver\lib\chromedriver\chromedriver.exe
    
    > core-js@2.6.9 postinstall E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\core-js
    > node scripts/postinstall || echo "ignore"
    
    Thank you for using core-js ( https://github.com/zloirock/core-js ) for polyfilling JavaScript standard library!
    
    The project needs your help! Please consider supporting of core-js on Open Collective or Patreon:
    > https://opencollective.com/core-js
    > https://www.patreon.com/zloirock
    
    Also, the author of core-js ( https://github.com/zloirock ) is looking for a good job -)
    
    
    > uglifyjs-webpack-plugin@0.4.6 postinstall E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\webpack\node_modules\uglifyjs-webpack-plugin
    > node lib/post_install.js
    
    npm notice created a lockfile as package-lock.json. You should commit this file.
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@^1.2.3 (node_modules\sane\node_modules\fsevents):
    npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.9: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})
    npm WARN ajv-keywords@2.1.1 requires a peer of ajv@^5.0.0 but none is installed. You must install peer dependencies yourself.
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: abbrev@1.1.1 (node_modules\fsevents\node_modules\abbrev):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\abbrev' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.abbrev.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: ansi-regex@2.1.1 (node_modules\fsevents\node_modules\ansi-regex):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\ansi-regex' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.ansi-regex.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: aproba@1.2.0 (node_modules\fsevents\node_modules\aproba):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\aproba' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.aproba.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: balanced-match@1.0.0 (node_modules\fsevents\node_modules\balanced-match):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\balanced-match' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.balanced-match.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: chownr@1.1.1 (node_modules\fsevents\node_modules\chownr):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\chownr' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.chownr.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: code-point-at@1.1.0 (node_modules\fsevents\node_modules\code-point-at):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\code-point-at' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.code-point-at.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: concat-map@0.0.1 (node_modules\fsevents\node_modules\concat-map):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\concat-map' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.concat-map.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: console-control-strings@1.1.0 (node_modules\fsevents\node_modules\console-control-strings):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\console-control-strings' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.console-control-strings.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: core-util-is@1.0.2 (node_modules\fsevents\node_modules\core-util-is):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\core-util-is' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.core-util-is.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: deep-extend@0.6.0 (node_modules\fsevents\node_modules\deep-extend):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\deep-extend' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.deep-extend.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: delegates@1.0.0 (node_modules\fsevents\node_modules\delegates):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\delegates' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.delegates.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: detect-libc@1.0.3 (node_modules\fsevents\node_modules\detect-libc):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\detect-libc' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.detect-libc.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fs.realpath@1.0.0 (node_modules\fsevents\node_modules\fs.realpath):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\fs.realpath' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.fs.realpath.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: has-unicode@2.0.1 (node_modules\fsevents\node_modules\has-unicode):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\has-unicode' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.has-unicode.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: inherits@2.0.3 (node_modules\fsevents\node_modules\inherits):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\inherits' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.inherits.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: ini@1.3.5 (node_modules\fsevents\node_modules\ini):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\ini' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.ini.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: isarray@1.0.0 (node_modules\fsevents\node_modules\isarray):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\isarray' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.isarray.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: minimist@0.0.8 (node_modules\fsevents\node_modules\minimist):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\minimist' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.minimist.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: ms@2.1.1 (node_modules\fsevents\node_modules\ms):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\ms' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.ms.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: npm-bundled@1.0.6 (node_modules\fsevents\node_modules\npm-bundled):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\npm-bundled' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.npm-bundled.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: number-is-nan@1.0.1 (node_modules\fsevents\node_modules\number-is-nan):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\number-is-nan' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.number-is-nan.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: object-assign@4.1.1 (node_modules\fsevents\node_modules\object-assign):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\object-assign' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.object-assign.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: os-homedir@1.0.2 (node_modules\fsevents\node_modules\os-homedir):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\os-homedir' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.os-homedir.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: os-tmpdir@1.0.2 (node_modules\fsevents\node_modules\os-tmpdir):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\os-tmpdir' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.os-tmpdir.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: path-is-absolute@1.0.1 (node_modules\fsevents\node_modules\path-is-absolute):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\path-is-absolute' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.path-is-absolute.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: process-nextick-args@2.0.0 (node_modules\fsevents\node_modules\process-nextick-args):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\process-nextick-args' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.process-nextick-args.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: minimist@1.2.0 (node_modules\fsevents\node_modules\rc\node_modules\minimist):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\rc\node_modules\minimist' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\rc\node_modules\.minimist.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: safe-buffer@5.1.2 (node_modules\fsevents\node_modules\safe-buffer):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\safe-buffer' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.safe-buffer.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: safer-buffer@2.1.2 (node_modules\fsevents\node_modules\safer-buffer):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\safer-buffer' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.safer-buffer.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: sax@1.2.4 (node_modules\fsevents\node_modules\sax):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\sax' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.sax.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: semver@5.7.0 (node_modules\fsevents\node_modules\semver):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\semver' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.semver.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: set-blocking@2.0.0 (node_modules\fsevents\node_modules\set-blocking):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\set-blocking' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.set-blocking.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: signal-exit@3.0.2 (node_modules\fsevents\node_modules\signal-exit):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\signal-exit' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.signal-exit.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: strip-json-comments@2.0.1 (node_modules\fsevents\node_modules\strip-json-comments):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\strip-json-comments' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.strip-json-comments.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: util-deprecate@1.0.2 (node_modules\fsevents\node_modules\util-deprecate):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\util-deprecate' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.util-deprecate.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: wrappy@1.0.2 (node_modules\fsevents\node_modules\wrappy):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\wrappy' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.wrappy.DELETE'
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: yallist@3.0.3 (node_modules\fsevents\node_modules\yallist):
    npm WARN enoent SKIPPING OPTIONAL DEPENDENCY: ENOENT: no such file or directory, rename 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\yallist' -> 'E:\贾晓娇\Documents\Projects\vue-test-2\node_modules\fsevents\node_modules\.yallist.DELETE'
    
    added 1741 packages from 1121 contributors in 127.697s
    
    
    Running eslint --fix to comply with chosen preset rules...
    # ========================
    
    
    > vue-test-2@1.0.0 lint E:\贾晓娇\Documents\Projects\vue-test-2
    > eslint --ext .js,.vue src test/unit test/e2e/specs "--fix"
    
    
    # Project initialization finished!
    # ========================
    
    To get started:
    
      cd vue-test-2
      npm run dev
    
    Documentation can be found at https://vuejs-templates.github.io/webpack
    
    ```

### 到项目目录 运行项目

    npm run dev

    
    > vue-test-2@1.0.0 dev E:\贾晓娇\Documents\Projects\vue-test-2
    > webpack-dev-server --inline --progress --config build/webpack.dev.conf.js
    
    12% building modules 22/31 modules 9 active ...ments\Projects\vue-test-2\src\App.vue{ parser: "babylon" } is deprecated; we now treat it as { parser: "bab 95% emitting
    
    DONE  Compiled successfully in 4251ms                                                                       11:57:12 AM
    
    I  Your application is running here: http://localhost:8080

### 项目结构

- build目录：构建项目命令所需要使用到的一些脚本文件和配置文件
- config目录：在vue-cli中会自动安装一个小型的express搭建的热重载web服务器，config里面就是关于这个服务器的相关配置，包括端口号等。
- dist目录：项目编译构建上线后的存放目录
- node_modules目录：npm 加载的项目依赖包存放目录
- src目录：项目源代码存放目录
    - assets: 放置一些图片，如logo等。
    - components: 目录里面放了一个组件文件，可以不用。
    - App.vue: 项目入口文件，我们也可以直接将组件写这里，而不使用 components 目录。
    - main.js：项目的核心文件。vue脚手架为我们自动生成的项目中设置的入口文件，在该入口文件中，做了一些项目初始化的工作
        - 引入 Vue
        - 引入必要的组件
        - 创建Vue实例。
    - 在项目开发过程中，我们的大部分任务是在src这个目录下完成的
- static目录：静态资源存放目录
- test	初始测试目录，可删除
- .xxxx文件	这些是一些配置文件，包括语法配置，git配置等。
- index.html	首页入口文件，你可以添加一些 meta 信息或统计代码啥的。
- package.json	项目配置文件。
- README.md	项目的说明文档，markdown 格式
