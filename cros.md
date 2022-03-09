module.exports = {  
    /* 部署生产环境和开发环境下的URL：可对当前环境进行区分，baseUrl 从 Vue CLI 3.3 起已弃用，要使用publicPath */  
    publicPath: "",  
    assetsDir: "static/lipin",  
    outputDir: "dist",  
    runtimeCompiler: true,  
    productionSourceMap: false,  
    /* webpack-dev-server 相关配置 */  
    devServer: {  
        /* 自动打开浏览器 */  
        open: true,  
        /* 设置为0.0.0.0则所有的地址均能访问 */  
        host: "127.0.0.1",  
        port: 8080,  
        https: false,  
        hotOnly: false,  
        /* 使用代理 */  
        proxy: {  
            '/': {  
                /* 目标代理服务器地址 */  
                target: "http://localhost:8081",  
                /* 允许跨域 */  
                changeOrigin: true,  
            },  
        },  
    },  
} 