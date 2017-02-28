# Collection API

![image](https://cloud.githubusercontent.com/assets/18228937/23403676/b88927fe-fde3-11e6-949f-1f46bf47de95.png)

## List 

### ArrayList ?
+ ArrayList là 1 trong số thành phần trong Collection , nó có thể tự động gia tăng kích thức của mình (mảng động)

### Vector ?
+ Giống ArrayList nhưng hỗ trợ đồng bộ 

### LinkList ?
+ Một Danh sách liên kết bảng chất thì giống mảng nhưng xét về mặt bộ nhớ thì khởi tạo nó tốn bộ nhớ hơn mảng 

### So sánh khác nhau và ưu nhược điểm của từng loại 

+ ArrayList và Vector thì vector sẽ chậm hơn do hỗ trợ synchronized
+ ưu điểm ArrayList 
  + truy cập ngẫu nhiên các phần tử nhanh
  + tìm kiếm nhanh
+ ưu điểm LinkList
 + thêm , xóa phần tử 
 
+ bảng hiệu suất giữa 2 loại:

 ![image](https://cloud.githubusercontent.com/assets/18228937/23403021/b2ce90c2-fde0-11e6-9928-840bc454a43f.png)
 
 ### Sử dụng thế nào :
 
+ Add: vector hay linklist đều giống nhau
 ```
  List arrList = new ArrayList();
        SinhVien sv = SinhVien.getInstance();
        sv.setMaSV(19);
        sv.setTenSV("deptrai");
        arrList.add("hien");
        arrList.add(sv);
        return arrList;
        
 ```
 
+ Duyệt có 3 cách duyệt 
 ```
 // Foreach
 for (Object object : list) {
            System.out.println("" + object);
        }
        // sử dụng for bình thường 
        for (int i = 0; i < list.size() ; i++) {
            Object object = list.get(i);
            System.out.println("" + object);
        }
        
        // sử dụng Iterator
        Iterator itr = list.iterator();
        while(itr.hasNext()){
             Object element = itr.next();
             System.out.print(element + " ");
        }
 ```
 
+ cơ chế hoạt động của Iterator như thế nào:
 + tạo 1 con trỏ đầu danh sách và truy xuất tuần tự từng phần tử trong danh sách đó

+ Việc add được bất kỳ phần tử nào vào list như trên có gì bất cập không ?
 + tất nhiên là có rồi vì cứ mỗi lần như vậy chúng ta lại phải ép kiểu nhiều trường hợp chúng ta không kiểm tra kỹ càng có thể 
 sinh ra lỗi vì thế ***Generic ra đời*** để đánh dấu list này chỉ lưu 1 đối tượng nào đó thôi .
 
## Set

+ set thì giống list ***nhưng một phần tử đưa vào được sắp xếp và không có lấy ra 1 phần tử bất kì như list mà phải lặp dần*** 
+ set ***không có tính trùng nhau*** nên nếu có add 2 hay nhiều phần tử trùng nhau vào set thì nó coi như 1 
+ Lưu ý : set thì không an toàn trong đa luồng 

### Sử Dụng thế nào ?

+ ADD giống như list
```
Set s = new HashSet();
        SinhVien sv = SinhVien.getInstance();
        sv.setMaSV(19);
        sv.setTenSV("deptrai");
        s.add("hien");
        s.add(sv);
```

+ Duyệt thì dùng iterator hoặc foreach
```
        for (Object object : set) {
            System.out.println("" + object);
        }
       
        Iterator itr = set.iterator();
        while(itr.hasNext()){
             Object element = itr.next();
             System.out.print(element + " ");
        }
```

https://viblo.asia/nguyen.van.ngoc/posts/AyQMpJ07v0Ek </br>
https://howtocodevn.wordpress.com/2015/11/05/java-su-khac-nhau-giua-treeset-linkedhashset-va-hashset/
