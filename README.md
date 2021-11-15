# mrh-dfs-spring-boot-autoconfigure

	对常用的文件存储，封装统一的文件存储客户端sdk

##### 客户端配置

	使用时需要在 application.properties 中指定客户端配置
	
	①，本地磁盘存储：
	
		dfs.disk.enabled=true
		dfs.disk.root-path=/usr/local/file
	
	②，ftp服务器存储：
		
		dfs.ftp.enabled=true
		dfs.ftp.charset=UTF-8
		dfs.ftp.connect-timeout-in-seconds=5
		dfs.ftp.host=127.0.0.1
		dfs.ftp.port=23
		dfs.ftp.username=user
		dfs.ftp.password=password
	
	③，腾讯云cos存储：
	
		dfs.cos.enabled=true
		dfs.cos.app-id=APPID
		dfs.cos.secret-id=KEY
		dfs.cos.secret-key=KEY
		dfs.cos.region=REGION
		dfs.cos.bucket=BUCKET
	
	④，fastdfs存储：
	
		dfs.fastdfs.enabled=true
		dfs.fastdfs.tracker-servers=
		dfs.fastdfs.http-tracker-http-port=
		dfs.fastdfs.charset=
		dfs.fastdfs.connect-timeout-in-seconds=
		dfs.fastdfs.http-anti-steal-token=
		dfs.fastdfs.http-secret-key=
		dfs.fastdfs.network-timeout-in-seconds=
		dfs.fastdfs.max-retris=

##### 使用示例

	注入文件客户端bean：
			
		@Autowired
		private FileStoreClient client;
	
	示例中，identify 文件系统标识当前文件的唯一ID.
	
	文件上传示例：
	
		try {
			UploadFileRequest request = new UploadFileRequest(buffers, originalName);
			UploadFileResponse response = client.uploadFile(request);
			String identify = response.getIdentity();
		} catch (FileStoreException e) {
			// TODO 上传失败
		}
	
	文件下载示例：
	
		try {
			DownloadFileRequest request = new DownloadFileRequest(identity);
			DownloadFileResponse response = client.downloadFile(request);
			byte[] buffer = response.getBuffers();
		} catch (FileStoreException e) {
			// TODO 下载失败
		}
	
	文件删除示例：
	
		try {
			DeleteFileRequest request = new DeleteFileRequest(identity);
			client.deleteFile(request);
		} catch (FileStoreException e) {
			// TODO 删除失败
		}

##### 后续集成和优化

	①，断点续传
	
	②，大文件处理
	
	③，其他存储客户端集成
