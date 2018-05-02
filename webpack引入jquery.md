## webpack 引入 jquery 插件

> 网上看了很多引用方法，可是每个试了都没成功，npm的时候直接error中断。不知道是方法本身导致的还是我某个细节遗漏了。

> 下面是我终于终于成功引入jquery的代码，怕下次使用是忘记，特此记录一下。

>> 首先，*npm install jquery --save-dev* 安装 jquery

>> 然后，

        plugins: [
                new webpack.ProvidePlugin({
                    $: "jquery",
                    jquery: "jQuery",
                    "windows.jQuery": "jquery"
                })
            ],
        resolve: {
                alias: {
                    jquery: 'jquery/src/jquery'
                }
            }


—————----—其他方法补充记录—————----—

    方法二：
        使用expose-loader

        module: {
            rules: [
              // any other rules
              {
                // Exposes jQuery for use outside Webpack build
                test: require.resolve('jquery'),
                use: [{
                  loader: 'expose-loader',
                  options: 'jQuery'
                },{
                  loader: 'expose-loader',
                  options: '$'
                }]
              }
            ]
          },
          plugins: [
            // Provides jQuery for other JS bundled with Webpack
            new webpack.ProvidePlugin({
              $: 'jquery',
              jQuery: 'jquery'
            })
          ]