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
+ ***Lưu ý*** : set thì không an toàn trong đa luồng , phải sử dụng synchronize bên ngoài nếu cần. 

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

### Sử khác nhau và các trường hợp dùng HashSet vs. TreeSet vs. LinkedHashSet
+ nói về hiệu xuất thì HashSet là nhanh nhất 
+ còn về sắp xếp thì nên chọn TreeSet
+ còn nếu muốn đọc một Set theo thứ tự mà các phần tử được insert vào thì dùng LinkedHashSet , vì LinkedHashSet sắp xếp theo thứ tự insert vào.
+ Cả 2 HashSet và LinkedHashSet cho phép phần tử null, nhưng TreeSet không cho phép và throws NullPointerExeption nếu insert null.

***HashSet***
+ HashSet được implement bằng cách sử dụng một hash table. Các thành phần không được sắp xếp theo thứ tự.

***TreeSet***
+ được implement bằng cách sử dụng cấu trúc dữ liệu tree, các thành phần trong Set được sắp xếp theo thứ tự.

***LinkedHashSet***
+  được implement như một hash table với mỗi phần tử trong bảng băm này sẽ trỏ đến phần tử đầu tiên của một Linked List. Vì vậy mà các phần tử có thể được sắp xếp.

+ ***lưu ý*** : đối với set nào có sự sắp xếp như TreeSet và LinkedHashSet khi ta thêm 1 đối tượng nào đó và thì phải implements Comparable và Override cho hàm compareTo 

```
class Dog implements Comparable{
int size;

public Dog(int s) {
size = s;
}

public String toString() {
return size + "";
}

@Override
public int compareTo(Dog o) {
        return size - o.size;
}
}
```
## Map 
+ Map là một tập dữ liệu được lưu dưới dạng key-value. Một Map không thể chứa những key trùng nhau, nhưng mỗi key thì có thể được ánh xạ đến nhiều hơn một giá trị.
+ HashMap không synchronize và không an toàn với đa luồng(not thread safe).

+ [Map hoạt động thế nào ?](https://kipalog.com/posts/Java-nhung-dieu-co-the-ban-da-biet--Map-HashMap-hoat-dong-nhu-the-nao)

### Sử Dụng thế nào ?


### HashMap và HashTable khác nhau thế nào 
![hashmap-hashtable](https://cloud.githubusercontent.com/assets/18228937/23584639/8035b08e-0199-11e7-81ae-37e7ca725cdd.png)

***HashMap***

***
