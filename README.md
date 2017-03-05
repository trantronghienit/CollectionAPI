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
        
  // forEach 1.8   // list.forEach(Comsumer)
   list.forEach(new Consumer<SinhVien>() {
           @Override
           public void accept(SinhVien t) {
               // t là 1 đối tượng khi mỗi lần lặp thì nó tra về 1 đối tượng chúng ta có thể dùng đối tượng để in ra hay so sánh ...
           }
       });
        
 //lamda
 ArrayList<SinhVien> list = new ArrayList();
       list.add(new SinhVien(1, "adad"));
       list.add(new SinhVien(2, "ad"));
       list.add(new SinhVien(3, "aadadd"));
       list.forEach(sv-> {
           sv.getMaSV();
           sv.getTenSV();
       });
 ```
 
+ Tìm Kiếm
 
+ So Sánh

+ Sắp Xếp


+ cơ chế hoạt động của Iterator như thế nào:
 + tạo 1 con trỏ đầu danh sách và truy xuất tuần tự từng phần tử trong danh sách đó

+ Việc add được bất kỳ phần tử nào vào list như trên có gì bất cập không ?
 + tất nhiên là có rồi vì cứ mỗi lần như vậy chúng ta lại phải ép kiểu nhiều trường hợp chúng ta không kiểm tra kỹ càng có thể 
 sinh ra lỗi vì thế ***Generic ra đời*** để đánh dấu list này chỉ lưu 1 đối tượng nào đó thôi .
 
## Set

+ set thì giống list ***nhưng một phần tử đưa vào được sắp xếp và không có lấy ra 1 phần tử bất kì như list mà phải lặp dần*** 
+ set ***không có tính trùng nhau*** nên nếu có add 2 hay nhiều phần tử trùng nhau vào set thì nó coi như 1 
+ ***Lưu ý*** :
  + set thì không an toàn trong đa luồng , phải sử dụng synchronize bên ngoài nếu cần. 
  + set thì do tính chất là so sánh nên nếu chúng ta cố tình add kiểu dữ liệu khác nhau vào Set nó sẽ báo lỗi
  + hoặc ta add vào 1 đối tượng nhưng chưa cài đè hàm compareTo cho object cũng dễ khiến sinh ra lỗi 

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
***1 . Lấy toàn bộ entry của Map***

```
 cách 1: for-each
 // tại sao map.entrySet() lại trả về 1 kiểu set ?
  Set<Map.Entry<Integer, SinhVien>> entrySet = map.entrySet();
        for (Map.Entry<Integer, SinhVien> entry : entrySet) {
             System.out.println("Key = " + entry.getKey() + ", Value = " + entry.getValue());
        }
// vì một entry là 1 set vì tính chất chúng không trùng nhau , nói cách khác vì Map là tập hợp nhiều set 
// - vì sao lại đánh dấu Map.Entry<Integer, SinhVien> => vì Entry nằm trong Map  , đánh dấu để biết set đó kiểu gì 

cách 2 : dùng Iterator 

Iterator<Map.Entry<Integer, SinhVien>> iterator = map.entrySet().iterator();
        while(iterator.hasNext()){
            Map.Entry<Integer, SinhVien> entry = iterator.next();
            System.out.println("Key = " + entry.getKey() + ", Value = " + entry.getValue());
        }
        
```

***2 . Lấy toàn bộ key của Map***
```
for (Integer key : map.keySet()) {
    System.out.println("Key = " + key);
}

//=============== Iterator =======
Iterator<Integer> iterator = map.keySet().iterator();
while (iterator.hasNext()) {
    Integer key = iterator.next();
    System.out.println("Key = " + key);
}
```

***3. Lấy toàn bộ value của Map***
```
for (Integer value : map.values()) {
    System.out.println("Value = " + value);
}

//==================

Iterator<Integer> iterator = map.values().iterator();
while (iterator.hasNext()) {
    Integer value = iterator.next();
    System.out.println("Value = " + value);
}

```

== > Có thể lấy toàn bộ key của Map, sau đó lấy value tương ứng .

### HashMap và HashTable khác nhau thế nào 
![hashmap-hashtable](https://cloud.githubusercontent.com/assets/18228937/23584639/8035b08e-0199-11e7-81ae-37e7ca725cdd.png)


## Quece </br>

Quece(hàng đợi) là một Interface con của Collection . nó khá giống với List, tuy nhiên mục đích sử dụng hơi khác nhau. Queue được thiết kế để bạn chỉ có thể truy cập phần tử ở đầu hàng đợi.

+ Là tập hợp cho phép các phần tử trùng lặp.
+ Không cho phép phần tử null.
+ Có hai class thi hành interface Queue.
 + java.util.LinkedList
  + java.util.PriorityQueue
  
![method](https://cloud.githubusercontent.com/assets/18228937/23585707/ca7c37da-01b7-11e7-81c8-30d186a84f9c.png)

+  offer(E)
Trèn phần tử vào hàng đợi nếu có thể làm điều đó ngay lập tức nếu không bị giới hạn bởi kích thước hàng đợi. Khi sử dụng hàng đợi có kích thước giới hạn, phương thức này khá giống với add(E), tuy nhiên phương thức này không ném ra ngoại lệ khi không trèn được phần tử vào hàng đợi, mà nó trả về false trong tình huống đó. 

+ add(E)
Trèn một phần tử vào hàng đợi nếu có thể làm điều này ngay lập tức mà không bị giới hạn bởi kích thước hàng đợi, trả về true nếu thành công, ngược lại nó sẽ ném ra ngoại lệ IllegalStateException khi hàng đợi không còn chỗ.

+ remove()
Lấy ra và loại bỏ luôn phần tử đầu tiên của hàng đợi. Phương thức này chỉ khác với poll() ở chỗ nếu hàng đợi không có phần tử ngoại lệ sẽ bị ném ra. 

+ poll()
Lấy ra và loại bỏ phần tử đầu tiên trong hàng đợi, hoặc trả về null nếu hàng đợi không có phần tử nào. 

+ element()
Lấy ra nhưng không loại bỏ phần tử đứng đầu của hàng đợi. Phương thức này chỉ khác với peek() là nó ném ra ngoại lệ nếu hàng đợi không có phần tử.

+ peek()
Lấy ra, nhưng không loại bỏ phần tử đầu tiên trong hàng đợi, hoặc trả về null nếu hàng đợi không có phần tử nào. 
