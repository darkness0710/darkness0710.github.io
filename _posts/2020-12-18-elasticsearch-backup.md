**Elasticsearch** cái tên ngày càng trở nên quen thuộc do sức mạnh về tốc độ tìm kiếm và khả năng mapping dữ liệu một cách nhanh chóng. Khi sử dụng Elasticsearch một trong những công việc chúng ta phải làm thường xuyên là Snapshot and Restore data.
Cách cài đặt Elatichsearch các bạn có thể xem tại đây: [Setup Elatichsearch](https://viblo.asia/p/elasticsearch-setup-in-ubuntu-bWrZnv8bZxw)
# 1. Snapshot 
**Elatichserach** cung cấp cho chúng ta module snapshot để tạo nhanh các bản snapshot lưu trữ các indices hoặc một phần hoặc toàn bộ các cluster tại một thời điểm nào đó.
Snapshot tỏ ra mạnh mẽ và hữu dụng nhưng có một vài khuyết điểm mà chúng ta phải lưu ý như sau:
* Snapshot tạo từ phiên bản 5.x có thể phục hồi trong phiên bản 6.x.
* Snapshot tạo từ phiên bản 2.x có thể phục hồi trong phiên bản 5.x.
* Snapshot tạo từ phiên bản 1.x có thể phục hồi trong phiên bản 2.x.
> Các snapshot không tương thích với các phiên bản thì không thể phục hồi được, hãy lưu ý điều này khi update các version mới cho elatichsearch.
> Snapshot chỉ là những bức ảnh chụp nhanh dùng để lưu trữ dữ liệu chứ không phải toàn bộ dữ liệu tại thời điểm đó. Nói một cách đơn giản hơn khi restore data nếu snapshot bị hỏng thì chúng ta đang phải gặp một vấn đề cực kì khó khăn (yaoming).

Đầu tiên chúng ta phải tiến hành tạo repositories để lưu trữ các snapshot, Elatichsearch cung cấp một số repositories khả dụng như sau:
* AWS (You can store the backups on S3)
* HPFS for Hadoop
* Azure Cloud

Ở bài viết này mình sử dụng repositories tại local cho đỡ config nhiều (yaoming). Kiểm tra xem chúng ta đã tạo ra các repositories nào chưa:
```
$ curl -XGET 'localhost:9200/_snapshot/_all?pretty=true'
```
Tạo thư mục lưu trữ các repositories:
```
$ mkdir /usr/share/elasticsearch/data_backup
```
Cấp quyền cho elatichsearch lưu trữ vào thư muc:
```
$ chown -R elasticsearch:elasticsearch /usr/share/elasticsearch/data_backup
```
Config elasticsearch.yml tại /etc/elasticsearch/elasticsearch.yml tạo đường dẫn tới thư mục trên bằng cách khai báo path.repo:
```
path.repo: ["/usr/share/elasticsearch/data_backup"]
```
Khởi dộng lại Elatichsearch:
```
$ sudo service elasticsearch restart
```
Mapping và khởi tạo snapshot với repositories trên:
```
$ curl -XPUT -H "Content-type: application/json" -d '{   
"type": "fs",
   "settings": {
       "compress" : true,
       "location": "/usr/share/elasticsearch/data_backup"
}
}' 'http://localhost:9200/_snapshot/test_backup'
```
Sử dụng snapshot trên lưu trữ toàn bộ cluster và các indices:
```
$ curl -XPUT 'localhost:9200/_snapshot/test_backup/snapshot_1?wait_for_completion=true'
```

# 2. Restore data
Việc restore data trong elatichsearch thì khá là dễ dàng nhờ có module restore.
Đầu tiên chúng ta phải đóng toàn bộ các index đang mở:
```
$ curl -XPOST 'localhost:9200/_all/_close'
```
Sử dụng snapshot phục hồi dữ liệu nhanh chóng:
```
$ curl -XPOST 'localhost:9200/_snapshot/test_backup/snapshot_1/_restore'
```
Mở lại toàn bộ index cũ: 
```
$ curl -XPOST 'localhost:9200/_all/_open'
```

Tài liệu tham khảo:
https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-snapshots.html
https://qbox.io/blog/elasticsearch-data-snapshots-restore-tutorial
