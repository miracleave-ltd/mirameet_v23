# 11. ⑪ WEBのコンテナに接続します
```
docker exec -it myapp_web_1 bash
```

<br><br>
# 12. ⑫ 以下を、１行ずつ実行します
```
rails g model Employee number:string name:string date:string
```
```
rails db:migrate
```
```
rails g controller Employees
```
<br><br>
# 13. ⑬ myapp\app\controllers　配下の以下のファイルを編集します
対象ファイル：employees_controller.rb
```
class EmployeesController < ApplicationController
  def index
    @employees = Employee.all
  end
end
```
<br><br>
# 14. ⑭ myapp\db　配下の以下のファイルを編集します
対象ファイル：seeds.rb
```
Employee.create(
  [
    {
      number: '001',
      name: 'Yamada',
      date: '2018/01/01',
    },
    {
      number: '002',
      name: 'Tanaka',
      date: '2019/04/01',
    },
    {
      number: '003',
      name: 'Sato',
      date: '2019/05/01',
    },
  ],
)
```
<br><br>
# 15. ⑮ ⑭のファイルを元にデータを作成します
```
rails db:seed
```
<br><br>
# 16. ⑯ myapp\config　配下の以下のファイルを編集します
対象ファイル：routes.rb
```
Rails.application.routes.draw do
  root to: 'employees#index'
  resources :employees
end
```
<br><br>
# 17. ⑰ 以下のコマンドで画面を作成します
```
touch app/views/employees/index.html.erb
```

<br><br>
# 18. ⑱ app/views/employees　配下の以下のファイルを編集します
対象ファイル：index.html.erb
```
<h1>List of employees</h1>

<table border="1" width="700" cellspacing="0" cellpadding="5" bordercolor="#333333" class="table table-hover">
  <thead class="thead-dark">
    <tr>
      <th bgcolor="#87cefa" class="align-middle" scope="col" width="100"><font size="+1" color="#FFFFFF">Employee no</font></th>
      <th bgcolor="#87cefa" class="align-middle" scope="col" width="400"><font size="+1" color="#FFFFFF">Name</font></th>
      <th bgcolor="#87cefa" class="align-middle" scope="col" width="150"><font size="+1" color="#FFFFFF">Hire date</font></th>
    </tr>
  </thead>


  <tbody>
    <% @employees.each do |employee| %>
      <tr scope="row">
        <td><%= employee.number %></td>
        <td><%= employee.name %></td>
        <td><%= employee.date %></td>
      </tr>
    <% end %>
  </tbody>
</table>
```
<br><br>
# 19. ⑲ 以下に接続して確認！
```
http://localhost:3000/
```
![image-20191121003744232](https://user-images.githubusercontent.com/53431136/69325948-53db6d00-0c8e-11ea-982e-650f9e31d71d.png)

<br>
このような画面が表示されたら完成！

<br><br><br>
# 20. おまけ

<br>

# 21. モデルから画面まで自動生成します

```
rails g scaffold Personal number:string name:string date:string
```
<br>

# 22. 追加したモデルの分テーブルを作成します

```
rails db:migrate
```
<br>

# 23. 以下に接続して確認！
```
http://localhost:3000/personals
```

<br>

![キャプチャ](https://user-images.githubusercontent.com/53431136/69335804-d40ace00-0ca0-11ea-9fe8-3a8f0cbd74c4.PNG)

