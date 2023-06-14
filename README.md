'''
Bài tập tự luyện
Để quản lý biên lai thu tiền điện, người ta cần các thông tin sau:
- Với mỗi biên lai: Thông tin về hộ sử dụng điện, chỉ số điện cũ, chỉ số mới, số tiền phải trả.
- Các thông tin riêng của từng hộ gia đình sử dụng điện: Họ tên chủ hộ, số nhà, mã số công tơ điện.
*Yêu cầu 1: Hãy xây dựng lớp khachHang để lưu trữ các thông tin riêng của mỗi hộ gia đình.
*Yêu cầu 2: Xây dựng lớp BienLai để quản lý việc sử dụng và thanh toán tiền điện của các hộ dân.
*Yêu cầu 3: Xây dựng các phương thức thêm, xoá, sửa các thông tin riêng của mỗi hộ sử dụng điện.
*Yêu cầu 4: Viết phương thức tính tiền điện cho mỗi hộ gia đình theo công thức: (số mới - số cũ ) *750
'''

class khachHang:
    def __init__(self, name='', num=0, ecode=0) -> None:
        self.name = name    
        self.num = num      # số nhà
        self.ecode = ecode  # mã số công tơ điện
    
    def __str__(self):
        return f'Họ tên chủ hộ:{self.name}\nSố nhà:{self.num}\nMã số công tơ điện:{self.ecode}'
    
    def add(self):
        self.name = input("Nhập họ tên chủ hộ: ")
        self.num = int(input("Số nhà: "))
        self.ecode = int(input("Mã số công tơ điện: "))

    # def find(self, maSo=0, lst=[]):
    #     searchResult = None
    #     for i in lst:
    #         if maSo == self.ecode:
    #             searchResult = i
    #     return searchResult
    
    

    

class BienLai:
    hoGD = khachHang()
    def __init__(self, hoGD=None, oldindex=0, newindex=0, cost=0) -> None:
        self.oldindex = oldindex   # chỉ số điện cũ
        self.newindex = newindex   # chỉ số điện mới
        self.cost = cost           # số tiền điện phải trả
        self.hoGD = hoGD

    def calculate(self):
        self.hoGD.add()
        self.oldindex = int(input("Nhập chỉ số điện cũ: "))
        self.newindex = int(input("Nhập chỉ số điện mới: "))
        self.cost = (self.newindex - self.oldindex)*5

    def delete(self,maSo=0,lst=[]):
        searchResult = False
        for i in lst:
            if maSo == i.hoGD.ecode:
                lst.remove(i)
                searchResult = True
        return searchResult
    
    def update(self,maSo=0, lst=[], n=0):
        searchResult = False
        for i in lst:
            if maSo == i.hoGD.ecode:
                searchResult = True
                if n == 1:
                    new_name = input("Nhập thông tin họ và tên chủ hộ mới: ")
                    i.hoGD.name = new_name
                elif n == 2:
                    new_num = int(input("Nhập thông tin số nhà mới: "))
                    i.hoGD.num = new_num
                elif n == 3:
new_ecode = int(input("Nhập thông tin mã số công tơ điện mới: "))
                    i.hoGD.ecode = new_ecode      
        return searchResult

    def show_bienlai(self):
        print(f'Họ tên chủ hộ:{self.hoGD.name}')
        print(f'Số nhà:{self.hoGD.num}')
        print(f'Mã số công tơ điện:{self.hoGD.ecode}')
        print(f'Chỉ số điện cũ:{self.oldindex}')
        print(f'Chỉ số điện mới:{self.newindex}')
        print("~~~~~~~~~~~~~~~~~")
        print(f'*Tổng tiền điện:{self.cost}')

def main():
    print("     CHƯƠNG TRÌNH QUẢN LÝ BIÊN LAI THU TIỀN ĐIỆN")
    print("*************************MENU**************************")
    print("**  1. Nhập thông tin hộ sử dụng điện trên biên lai  **")
    print("**  2. Xóa thông tin hộ sử dụng điện                 **")
    print("**  3. Sửa thông tin hộ sử dụng điện                 **")
    print("*******************************************************")
    

    lst = []
    while 1:
        choice = int(input("Nhập tùy chọn: "))
        if choice == 1:
            n = int(input("Nhập số hộ muốn thêm: "))
            for i in range(n):
                hoGD = khachHang()
                bill = BienLai(hoGD)
                bill.calculate()
                lst.append(bill)
            for item in lst:
                print("---------------------------")
                print("Thông tin biên lai")
                item.show_bienlai()

        elif choice == 2:
            maSo = int(input("Nhập mã số công tơ điện của hộ muốn xóa: "))
            if BienLai().delete(maSo,lst) == True:
                print("Đã xóa thông tin hộ gia đình!")
            else:
                print("Không tìm thấy thông tin hộ gia đình!")


        elif choice == 3:
            newbill = BienLai()
            print("Sửa thông tin in trên biên lai (1,Chủ hộ / 2,Số nhà / 3,Mã số công tơ điện)")
            n = int(input("Chọn thông tin muốn sửa: "))
            maSo = int(input("Nhập mã số công tơ điện của hộ muốn sửa: "))
            if newbill.update(maSo,lst,n) == True:
                print("Đã sửa thông tin thành công!")
            else:
                print("Không tìm thấy thông tin hộ gia đình!")
  
        choice2 = int(input("Bạn có muốn tiếp tục không chương trình (1/Có  2/Không): "))
        if choice2 == 1:
            continue
        if choice2 == 2:
            break

main()
