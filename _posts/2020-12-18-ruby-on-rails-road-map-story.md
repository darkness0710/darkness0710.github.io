# 1.Lời nói đầu




"Ruby được thiết kế bởi **Yukihiro Matz Matsumoto** với mục đích '**làm cho lập trình viên hạnh phúc**", còn Ruby on Rails là **framework Rails** nó cung cấp nhiều magic mang lại nhiều lợi ích trong việc phát triển ứng dụng, tuy nhiên nó cũng gây khó khăn cho những người mới làm quen. Ruby on rails phức tạp hơn so với chúng ta tưởng tượng, thời gian đầu có thể sẽ khiến bạn bối rối vì có quá nhiều thứ phải học, hoặc không hiểu tại sao lại chạy được. Lúc đầu thì rất là khó khăn, nhưng càng đi sâu thì lại càng khó khăn hơn, lắm lúc chỉ muốn " **đập cái bàn**". 
Khi bắt đầu tìm hiểu Rails thì chúng ta sẽ được quăng ngay cuốn **RUBY ON RAILS TUTORIAL (RAILS 5) - Learn Web Development with Rails - by Michael Hart**l ( phiên bản có thể khác nhau). Cuốn sách này cung cấp kiến thức nền tảng cơ bản cho chúng ta - 1 phần so với sự phức tạp và đồ sộ trên con đường đầy khó nhằn mà chúng ta phải đi qua. Nếu ai đó nói với bạn học rails dễ lắm thì chỉ có thể là mấy bà HR chuyên chém gió, và đây có thể là những thứ bạn phải học để chinh phục Rails.
![](https://viblo.asia/uploads/2175763d-b3fd-46cb-8f9a-d616b82dd3bc.png)
Tác giả blogger **Kakubei's Rants** đã từng có nhận xét thế này về rails:
* **Đủ dễ** để làm cái gì đó nhỏ, như ý tưởng trong lúc uống cafe sáng của bạn chẳng hạn
* **Đủ khó** để 4 năm kinh nghiệm vẫn cảm thấy nó còn nhiều thứ để tìm hiểu
* **Đủ chuẩn** để làm việc một cách khoa học
* **Đủ lỏng** **lẻo** để apply anti-pattern nếu thích
* **Đủ đẹp** để bạn cảm thấy yêu công việc lập trình hơn
* **Đủ xấu** để bạn biết cần có một cái nhìn khách quan hơn
* **Đủ mạnh** để làm bất cứ (hầu hết) điều gì mà nền tảng web có thể mang lại cho người dùng
* **Đủ yếu** để bạn quay lưng tìm tới 1 chân trời khác (rồi sau đó trở lại, cảm thấy yêu Rails hơn)

# 2. Từng bước chinh phục rails

Chúng ta có thể kiên trì bao lâu với rails hay là sẽ quay lưng để tìm 1 chân trời khác? Tôi nghĩ học ngôn ngữ nào hay framework nào cũng vậy thôi nếu không đủ kiên nhẫn thì về quê lấy vợ =)). Bỏ qua sự phức tạp của rails chúng ta sẽ từng bước từng bước một chinh phục rails. Tôi nghĩ bài viết này sẽ cung cấp những thứ mà bạn có thể sẽ vấp phải khi tiến hành những project đầu tiên. Bài viết tổng hợp kiến thức từ nhiều nguồn và kinh nghiệm của bản thân nên sai sót là khó có thể tránh khỏi. Vì thế hãy tự mình kiểm chứng lại nhé ^^ Dưới đây là những thứ cơ bản mà chúng ta cần biết khi làm những project đầu tiên.
**`"Nếu bạn không thể giải thích điều gì một cách đơn giản thì chính bạn cũng không hiểu điều đó”- Albert Einstein`**

### 2.1 Gemfile
Giả sử chúng ta có một file Gemfile như sau:
```
source 'https://rubygems.org'

git_source(:github) do |repo_name|
  repo_name = "#{repo_name}/#{repo_name}" unless repo_name.include?("/")
  "https://github.com/#{repo_name}.git"
end


# Bundle edge Rails instead: gem 'rails', github: 'rails/rails'
gem 'rails', '~> 5.1.1'
# Use sqlite3 as the database for Active Record
gem 'sqlite3'
# Use Puma as the app server
gem 'puma', '~> 3.7'
# Use SCSS for stylesheets
gem 'sass-rails', '~> 5.0'
# Use Uglifier as compressor for JavaScript assets
gem 'uglifier', '>= 1.3.0'
# See https://github.com/rails/execjs#readme for more supported runtimes
# gem 'therubyracer', platforms: :ruby

# Use CoffeeScript for .coffee assets and views
gem 'coffee-rails', '~> 4.2'
# Turbolinks makes navigating your web application faster. Read more: https://github.com/turbolinks/turbolinks
gem 'turbolinks', '~> 5'
# Build JSON APIs with ease. Read more: https://github.com/rails/jbuilder
gem 'jbuilder', '~> 2.5'
# Use Redis adapter to run Action Cable in production
# gem 'redis', '~> 3.0'
# Use ActiveModel has_secure_password
# gem 'bcrypt', '~> 3.1.7'

# Use Capistrano for deployment
# gem 'capistrano-rails', group: :development

group :development, :test do
  # Call 'byebug' anywhere in the code to stop execution and get a debugger console
  gem 'byebug', platforms: [:mri, :mingw, :x64_mingw]
  # Adds support for Capybara system testing and selenium driver
  gem 'capybara', '~> 2.13'
  gem 'selenium-webdriver'
end

group :development do
  # Access an IRB console on exception pages or by using <%= console %> anywhere in the code.
  gem 'web-console', '>= 3.3.0'
  gem 'listen', '>= 3.0.5', '< 3.2'
  # Spring speeds up development by keeping your application running in the background. Read more: https://github.com/rails/spring
  gem 'spring'
  gem 'spring-watcher-listen', '~> 2.0.0'
end

# Windows does not include zoneinfo files, so bundle the tzinfo-data gem
gem 'tzinfo-data', platforms: [:mingw, :mswin, :x64_mingw, :jruby]
 
```
Như một thói quen chúng ta sẽ tiến hành xóa các comments và thay dấu single quote => double quote và sẽ thu được kết quả như này:
```
source "https://rubygems.org"

git_source(:github) do |repo_name|
  repo_name = "#{repo_name}/#{repo_name}" unless repo_name.include?("/")
  "https://github.com/#{repo_name}.git"
end

gem "rails", "~> 5.1.1"
gem "sqlite3"
gem "puma", "~> 3.7"
gem "sass-rails", "~> 5.0"
gem "uglifier", ">= 1.3.0"
gem "coffee-rails", "~> 4.2"
gem "turbolinks", "~> 5"
gem "jbuilder", "~> 2.5"

group :development, :test do
  gem "byebug", platforms: [:mri, :mingw, :x64_mingw]
  gem "capybara", "~> 2.13"
  gem "selenium-webdriver"
end

group :development do
  gem "web-console", ">= 3.3.0"
  gem "listen", ">= 3.0.5", "< 3.2"
  gem "spring"
  gem "spring-watcher-listen", "~> 2.0.0"
end

gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]

```
Trông có vẻ ok rồi đấy? Nhưng như vậy là chưa đủ, chúng ta nên sắp xếp cái khối gem theo thứ tự alphabet như này ( Trong sublime3 thì bôi đen nhấn F9 nhé - đừng như a bạn cùng project của tôi sắp xếp thủ công bằng tay )
Kết quả: 
```
source "https://rubygems.org"

git_source(:github) do |repo_name|
  repo_name = "#{repo_name}/#{repo_name}" unless repo_name.include?("/")
  "https://github.com/#{repo_name}.git"
end

gem "coffee-rails", "~> 4.2"
gem "jbuilder", "~> 2.5"
gem "puma", "~> 3.7"
gem "rails", "~> 5.1.1"
gem "sass-rails", "~> 5.0"
gem "sqlite3"
gem "turbolinks", "~> 5"
gem "uglifier", ">= 1.3.0"

group :development, :test do
  gem "byebug", platforms: [:mri, :mingw, :x64_mingw]
  gem "capybara", "~> 2.13"
  gem "selenium-webdriver"
end

group :development do
  gem "listen", ">= 3.0.5", "< 3.2"
  gem "spring"
  gem "spring-watcher-listen", "~> 2.0.0"
  gem "web-console", ">= 3.3.0"
end

gem "tzinfo-data", platforms: [:mingw, :mswin, :x64_mingw, :jruby]

```
### 2.2 Xây dựng static pages bằng kĩ thuật mới 
Chúng ta sẽ tiến hành xây dựng các trang tĩnh bằng kĩ thuật này: [xem chi tiết](https://viblo.asia/p/ky-thuat-tao-cac-trang-tinh-static-pages-trong-rails-LzD5dP8z5jY) mà anh Nguyễn Huy Hùng đã hướng dẫn thay cho cách viết cũ trong tutorial.

### 2.3 Sự khác nhau giữa resources và resource 
Các bạn có thể thấy sự khác biệt trong ví dụ sau đây:
```
resources :orders
=> rake routes

     orders GET        /orders(.:format)            orders#index
            POST       /orders(.:format)            orders#create
  new_order GET        /orders/new(.:format)        orders#new
 edit_order GET        /orders/:id/edit(.:format)   orders#edit
      order GET        /orders/:id(.:format)        orders#show
            PUT        /orders/:id(.:format)        orders#update
            DELETE     /orders/:id(.:format)        orders#destroy

resource :order
=> rake routes
      order POST       /order(.:format)            orders#create
  new_order GET        /order/new(.:format)        orders#new
 edit_order GET        /order/:id/edit(.:format)   orders#edit
            GET        /order/:id(.:format)        orders#show
            PUT        /order/:id(.:format)        orders#update
            DELETE     /order/:id(.:format)        orders#destroy
```

### 2.4 Sự khác nhau giữa find và find_by? 
Khi cùng tìm thấy bản ghi thì kết quả giữa **find** và **find_by** là như nhau:
![](https://viblo.asia/uploads/dbdda91a-c149-446d-8f74-4e0263cf92b1.png)
Khi không tìm thấy bản ghi thì chúng ta sẽ thấy sự khác biệt:
![](https://viblo.asia/uploads/b90c9c8f-c59e-4b3c-81e0-5ef800b60473.png)
**Find_by**: Trả về kết quả là **nil**
**Find**: Trả về kết quả là **ActiveRecord::RecordNotFound exception.**

### **2.5 Sự khác nhau giữa member route and collection route?**
Giả sử chúng ta có một file config/routes.rb như sau:
```
  resources :employees do
    member do
      get :preview
    end
    collection do
      get :search
    end
  end
```
Tiến hành chạy  `$ rake routes | grep employees`
![](https://viblo.asia/uploads/f3a081d7-5b1a-4a55-8df4-e5f994203fec.jpg)
Sự khác biệt là gì? Có lẽ các bạn sẽ tự tìm được câu trả lời khi nhìn kĩ vào hình!

### **2.6 Sự khác nhau giữa destroy và delete?**
Cả 2 phương thức trên đều xóa bản ghi từ database và sự khác biệt là:
**Delete**: Không gọi callback mà tiến hành xóa bản ghi từ database.
**Destroy**: Thực hiện gọi callback ví dụ before_destroy sau đó mới tiền hành xóa bản ghi từ db. 
Các bạn có thể đọc về callback: [tại đây](https://viblo.asia/p/callback-trong-rails-de-lam-gi-WkXRMpjYGba).

### **2.7 Sự khác nhau giữa count, length và size?**
Các bạn có thể xem chi tiết: [tại đây](https://viblo.asia/p/phan-biet-size-length-count-trong-rails-MdZkAjRDvox)
 **Lưu ý**:  3 thằng trên đều thuộc lớp `ActiveRecord::Relation` của Rails nhé!

### **2.8 Sự khác nhau giữa new, create, save?**
* **new**: Tạo mới một object nhưng chưa lưu vào database
* **create**:  Tạo mới một object và lưu vào database 1 lần
* **save**: Lưu object nếu object là một bản ghi mới được tạo ra trong cơ sở dữ liệu, nếu không sẽ tiến hành cập nhật mới.

### **2.9 Sự khác nhau giữa nil?, empty?, blank? and present? methods?**
Các bạn có thể xem chi tiết: [tại đây](https://viblo.asia/p/nil-empty-blank-va-present-trong-ror-XQZGxWDVvwA)

### **2.10 Sự khác nhau giữa class method và scope?**
Các bạn có thể xem chi tiết: [tại đây](https://viblo.asia/p/scope-va-class-method-trong-ruby-on-rails-rEBRAKALG8Zj)

### **2.11 Vấn đề N + 1 query trong rails và cách giải quyết?**
Các bạn có thể xem chi tiết: [tại đây](https://viblo.asia/p/eager-loading-in-rails-4-57rVRqqVR4bP)

### **2.12 Sự khác nhau giữa inner join và subquery?**
Các bạn có thể xem chi tiết: [tại đây](https://viblo.asia/p/join-vs-subquery-the-problem-of-mysql-query-optimizer-mrDGMbgXezL)

### **2.13 MVC trong rails?**
Cứ 100 người thì 99 người hiểu sai về MVC .
Đừng đi vào vết xe đổ của 99 người khác. Hãy đọc lại lần nữa về MVC? Bạn có chắc bạn đang hiểu đúng về MVC?
Các bạn có thể xem chi tiết: [tại đây](https://techmaster.vn/posts/7169/mo-hinh-mvc-trong-rails)

### **2.14 Sự khác nhau giữa render và redirect_to?**
Render có thể được sử dụng theo nhiều cách, nhưng chủ yếu được sử dụng để render các khung  html của bạn. 
```
#index.html.erb 
<%= render @users %>

#_user.html.erb
<%= user.name %>
```
Còn redirect_to sẽ điều hướng trang tới liên kết của bạn:
```
redirect_to "https://www.google.com/"
```

### **2.15 Các kiểu liên kết trong rails?**
Các bạn có thể xem chi tiết: [tại đây](https://techtalk.vn/cac-kieu-lien-ket-rails-trong-ruby.html)

### **2.16 Validation trong rails?**
Các bạn có thể xem chi tiết: [tại đây](https://viblo.asia/p/tong-hop-cac-cach-su-dung-validation-trong-rails-z3NVRkK5R9xn)

### **3. Kết luận**
Trong rails còn vô vàn các loại kĩ thuật cũng như 1 bảo tàng các gem cần phải tìm hiểu. Trên đây là những điều cơ bản nhất là tiền đề đầu tiên trên con đường chinh phục rails. Mọi thắc mắc các bạn có thể search google =)) Hẹn gặp lại vào những bài viết sau ^^
