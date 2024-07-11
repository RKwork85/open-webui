# 关于open-webui的仓库记录





## bugs

1 不能够链接ollama下载模型

solution:

ollama服务启动错误,需配置外部访问

    export OLLAMA_HOST=0.0.0.0:11434
    ollama serve 


2  不可以上传文档

>Failed to load resource: the server responded with a status of 422

description:

1 在对话界面中上传文档信息，一直显示为加载

2 在工作空间-文档界面上传后没有任何提示，浏览器控制台报上述错误

solution:

1 在管理员设置面板-模型中下载语义向量模型 bge-large-zh

2 在管理员设置面板-文档中语义向量模型引擎选择ollama 后选择下载好的语义向量模型  最后  设置 块大小 块重叠  分别设为 200 50

 




## questions

如何查看一个docker容器的大小    24.1MB (virtual 3.62GB)
如何查看一个docker镜像的大小    3.59G
本地存储剩余                    170G



3 语义向量模型 对大文本无法理解 

原模型 sentence-transformers/all-MiniLM-L6-v2 

size: 22mb

solution: 换模型试试

4 语义向量模型无法下载

description：

Something went wrong :/ We couldn't connect to 'https://huggingface.co' to load this file, couldn't find it in the cached files and it looks like quentinz/bge-large-zh-v1.5 is not the path to a directory containing a file named config.json. Checkout your internet connection or see how to run the library in offline mode at 'https://huggingface.co/docs/transformers/installation#offline-mode'.

solution：


上传成功示例
![alt text](image.png)

5 大文件上传较慢支持pdf(18M) 5min以上？


6 search配置失败

HTTPConnectionPool(host='searxng', port=8080): Max retries exceeded with url: /search?q=%E5%B9%BF%E5%B7%9E%E4%BB%8A%E5%A4%A9%E5%A4%A9%E6%B0%94%E6%80%8E%E4%B9%88%E6%A0%B7&format=json&pageno=1&safesearch=1&language=en-US&time_range=&categories=&theme=simple&image_proxy=0 (Caused by NameResolutionError("<urllib3.connection.HTTPConnection object at 0x74f1cc1e7950>: Failed to resolve 'searxng' ([Errno -2] Name or service not known)"))

启动服务：

docker run -d --name searxng -p 8080:8080 -v ./searxng:/etc/searxng --restart always searxng/searxng:latest



7 sd图片生成

docker run -d -p 3000:8080 --add-host=host.docker.internal:host-gateway -e AUTOMATIC1111_BASE_URL=http://host.docker.internal:7861/ -e ENABLE_IMAGE_GENERATION=True -v open-webui:/app/backend/data --name open-webui --restart always ghcr.io/open-webui/open-webui:main

cd /home/rkwork/work_place/project/stable-diffusion-webui

./webui.sh --api --listen


## others

1 更新镜像版本

第一次下载的镜像id:

"Id": "sha256:3d903846dc81f9a4b7789f0b20a712f307258cf5d9b6a1d0f18c738599498def",

更新order：

docker pull ghcr.io/open-webui/open-webui:main


2 其他命令：

列出所有已创建的数据卷

- docker volume ls

数据卷在宿主机上的实际挂载路径

- docker volume inspect open-webui


3 配置搜索

https://programmablesearchengine.google.com/controlpanel/all

Custom Search JSON API：
AIzaSyCiRa0ZsUP5ell6VvoJB9f-jCL0SOYgJ78
id:
a13b2b55e8fe145f2