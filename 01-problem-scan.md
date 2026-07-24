# 01 - Problem Scan & Quick Cards

## Thong tin ca nhan

- Ho va ten: Nguyen Cong Hung
- MSSV: 2A202601071
- Nhom: Brick by brick

---

# Phase 1 - SCAN: Tim kiem co hoi

Hay su dung 4 lenses de quet qua hoat dong van hanh cua cac cong ty thanh vien Vingroup. Ghi lai it nhat 5 bai toan/bottleneck thuc te.

## List bai toan cua toi

| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mo ta ngan bai toan |
|---|----------------------------------|------|---------------------|
| 1 | VinFast | Lap lai (Repetitive) | Co van dich vu phai doc ho so bao hanh, anh loi va lich su sua chua de phan loai yeu cau, gay cham tiep nhan. AI co the trich xuat thong tin, doi chieu dieu kien bao hanh va de xuat nhom xu ly. |
| 2 | Xanh SM | Ton thoi gian (Time-consuming) | Nhan vien van hanh phai doi soat khieu nai chuyen xe tu GPS, cuoc phi, cuoc goi va phan hoi tai xe, gay ton dong ho so. AI co the tong hop bang chung va tao ket luan so bo de rut ngan SLA xu ly. |
| 3 | Vinhomes | Pain tu nguoi khac (Stakeholder Pain) | Cu dan va ban quan ly phai trao doi nhieu vong de lam ro yeu cau sua chua, gay cho doi va dieu phoi sai ky thuat vien. AI co the chuan hoa noi dung, xac dinh hang muc va muc uu tien. |
| 4 | Vinmec | AI co the tot hon (AI-upgrade) | Dieu duong phai doc tai lieu kham truoc, don thuoc va ket qua xet nghiem de chuan bi ho so, co nguy co bo sot thong tin. AI co the trich xuat du lieu, phat hien truong con thieu va tao ban tom tat. |
| 5 | Vinpearl | Lap lai (Repetitive) | Nhan vien buong phong phai kiem tra thu cong danh muc tien nghi va tinh trang phong truoc khi ban giao, gay bo sot va cham quay vong phong. AI co the doi chieu anh kiem tra voi checklist. |

---

# Phase 2 - QUICK-ASSESS: 3 Quick Problem Cards

Chon top 3 tu danh sach SCAN: #2 (Xanh SM doi soat khieu nai chuyen xe), #3 (Vinhomes chuan hoa yeu cau sua chua), #4 (Vinmec chuan bi ho so truoc kham).

## The bai toan tieu bieu: Card #2 - Xanh SM doi soat khieu nai chuyen xe

```text
QUICK PROBLEM CARD #2

Bai toan:
Nhan vien van hanh Xanh SM phai tong hop nhieu nguon du lieu de xac minh
va xu ly khieu nai cua mot chuyen xe.

Cong ty thanh vien:
[ ] VinFast  [x] Xanh SM  [ ] Vinhomes  [ ] Vinmec  [ ] Khac

Ai dang dau?
- Nhan vien van hanh/CSKH: mat thoi gian doi soat ho so.
- Khach hang: phai cho ket qua xu ly khieu nai.
- Tai xe: can ket luan minh bach va co du bang chung.

Workflow thu cong hien tai (5 buoc):
1. Tiep nhan ticket va xac dinh ma chuyen xe
-> 2. Mo du lieu GPS, lo trinh, cuoc phi va thanh toan
-> 3. Nghe cuoc goi, doc ghi chu khach hang va tai xe
-> 4. Doi chieu bang chung voi chinh sach xu ly
-> 5. Viet ket luan, phan hoi va cap nhat trang thai ticket

Buoc nao ton thoi gian/loi nhat?
Buoc 3-4, uoc tinh 12-18 phut/ho so.

AI co the nhay vao ho tro o buoc nao?
Buoc 3-5: chuyen loi noi thanh van ban, tom tat bang chung, phat hien
diem mau thuan va tao draft ket luan. Nhan vien van phai phe duyet
hoan tien, boi thuong hoac xu phat.

Do thanh cong bang gi (Metric co so)?
Giam thoi gian xu ly trung vi tu 20 phut xuong duoi 8 phut; it nhat
90% draft chua du cac nguon bang chung bat buoc.

Quick Architecture:
[ ] No AI  [x] Rule  [x] LLM  [ ] Agent
Rule doi soat GPS/cuoc phi; LLM xu ly cuoc goi va ghi chu tu do.
```

---

## The bai toan tieu bieu: Card #3 - Vinhomes chuan hoa va route yeu cau sua chua

```text
QUICK PROBLEM CARD #3

Bai toan:
Yeu cau sua chua cua cu dan thuong thieu thong tin, khien ban quan ly
phai hoi lai va co the dieu phoi sai doi xu ly.

Cong ty thanh vien:
[ ] VinFast  [ ] Xanh SM  [x] Vinhomes  [ ] Vinmec  [ ] Khac

Ai dang dau?
- Cu dan: phai mo ta lai su co va cho xu ly lau hon.
- Nhan vien CSKH/BQL: phai hoi bo sung va phan loai thu cong.
- Ky thuat vien: co the nhan ticket sai chuyen mon hoac thieu dung cu.

Workflow thu cong hien tai (5 buoc):
1. Cu dan gui noi dung, anh hoac ghi am ve su co
-> 2. CSKH doc va lien he hoi them thong tin
-> 3. Phan loai hang muc va danh gia muc do khan cap
-> 4. Chon doi ky thuat/nha thau phu hop
-> 5. Tao lich hen va chuyen ticket de xu ly

Buoc nao ton thoi gian/loi nhat?
Buoc 2-4, uoc tinh 8-15 phut/yeu cau, chua tinh thoi gian cho.

AI co the nhay vao ho tro o buoc nao?
Buoc 1-4: trich xuat can ho/vi tri, loai su co, muc khan cap; phat
hien thong tin con thieu; tao cau hoi bo sung va de xuat doi xu ly.

Do thanh cong bang gi (Metric co so)?
Giam thoi gian phan loai tu 10 phut xuong duoi 2 phut; tang ty le
route dung ngay lan dau tu 75% len it nhat 90%.

Quick Architecture:
[ ] No AI  [x] Rule  [x] LLM  [ ] Agent
LLM hieu mo ta tu do; rule kiem tra SLA, muc khan cap va tuyen xu ly.
```

---

## The bai toan tieu bieu: Card #4 - Vinmec chuan bi ho so truoc buoi kham

```text
QUICK PROBLEM CARD #4

Bai toan:
Dieu duong phai doc nhieu tai lieu y te de chuan bi ban tom tat truoc
kham va kiem tra cac thong tin con thieu.

Cong ty thanh vien:
[ ] VinFast  [ ] Xanh SM  [ ] Vinhomes  [x] Vinmec  [ ] Khac

Ai dang dau?
- Dieu duong: mat thoi gian tim va tong hop thong tin.
- Bac si: co the nhan ho so thieu hoac kho doc nhanh.
- Nguoi benh: co nguy co phai bo sung giay to vao sat gio kham.

Workflow thu cong hien tai (5 buoc):
1. Mo ho so kham cu va tai lieu nguoi benh cung cap
-> 2. Doc chan doan, dien bien va chi dinh gan nhat
-> 3. Tong hop thuoc, di ung va ket qua xet nghiem
-> 4. Kiem tra truong bat buoc con thieu hoac da qua han
-> 5. Viet ban tom tat de bac si ra soat truoc buoi kham

Buoc nao ton thoi gian/loi nhat?
Buoc 2-4, uoc tinh 15-25 phut/benh nhan co ho so phuc tap.

AI co the nhay vao ho tro o buoc nao?
Buoc 2-5: trich xuat du lieu co cau truc, canh bao truong thieu va
tao ban tom tat co dan chieu ve tai lieu goc. Dieu duong/bac si bat
buoc xac nhan truoc khi su dung.

Do thanh cong bang gi (Metric co so)?
Giam thoi gian chuan bi trung vi tu 20 phut xuong duoi 7 phut; 100%
ban tom tat AI duoc nhan vien y te duyet truoc khi su dung.

Quick Architecture:
[ ] No AI  [x] Rule  [x] LLM  [ ] Agent
Rule kiem tra truong bat buoc; LLM tom tat co dan nguon, khong chan doan.
```
