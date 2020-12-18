## Một số vấn đề thường gặp trong Bournce Shell
# 1. Sử dụng $* hay $@?
Khi bạn muốn lấy toàn bộ biến truyền vào trong file thực thi shell. Chúng ta sẽ có 2 sự lựa chọn:
- $*
- $@

Trong 1 số trường hợp bình thường thì nó sẽ giống nhau, nhưng 1 số TH đặc biệt có dấu quote thì nó sẽ khác nhau:

test.sh
```
#!/bin/bash
echo "With *:"
for arg in "$*"; do echo "<$arg>"; done

echo "With @:"
for arg in "$@"; do echo "<$arg>"; done
```
sh test.sh 1 2 "3 4"

Kết quả thu được là:
```
With *:
<1 2 3 4>
With @:
<1>
<2>
<3 4>
```
# 2. Return value trong function?
Khi chúng ta muốn lấy 1 return từ 1 hàm thông thường chúng ta sẽ làm như sau:

test.sh
```
#!/bin/bash
sumNumber () {
    return `expr $0 + $1`
}
result = sumNumber()
echo $result
```

Hmm ... toang. Shell không trả về giá trị như cái cách chúng ta nghĩ ...

Giải pháp 1. Sử dụng toán tử $?
```
#!/bin/bash
sumNumber () {
    return $(($1+$2))
}
sumNumber $1 $2
result=$?
echo $result
```

Giải pháp2. Sử dụng echo
#!/bin/bash
sumNumber () {
    echo $(($1+$2))
}
result=$(sumNumber $1 $2)
echo $result

Giải pháp3. Sử dụng biến global
```
#!/bin/bash
a=$1
b=$2
result=''
sumNumber () {
    result=$((a+b))
}
sumNumber
echo $result
```
