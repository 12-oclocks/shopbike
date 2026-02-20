# ShopBike - Core Handover (No Training / No Doc Rules)

Tai lieu nay la nguon su that de code va review cho du an ShopBike.
Muc tieu: giu dung business logic cot loi, bo qua cac tai lieu training/hoc thuat.

## 1) Project nature

ShopBike la marketplace mua ban xe dap cu co kiem dinh.

Flow chinh:

Seller -> Inspector -> Buyer -> Transaction -> Sold

## 2) Tech stack (thuc te dang dung)

- React + TypeScript
- React Router v6
- Zustand
- Axios
- Tailwind
- Backend REST API `/api/...`

Khong rang buoc UI/UX Pro Max, khong bat buoc pattern hoc thuat phuc tap.
UI chi can ro rang, de dung.

## 3) Authentication (muc thuc te)

- Dung Zustand luu `accessToken`
- Co `RequireAuth`
- Co `GuestGuard`
- Logout phai clear token

## 4) API layer

- Co `apiClient`
- Interceptor attach token
- Co the co refresh token neu can
- Component nen goi qua service layer

## 5) Business logic cot loi (khong duoc sai)

### Publish rule

Listing chi duoc `Published` khi Inspector `APPROVE`.

### Inspection decision

Inspector co 3 ket qua:

- `APPROVE` -> Publish
- `REJECT` -> Ket thuc
- `NEED_UPDATE` -> Tra ve Seller sua

### Listing states

- Draft
- Pending Inspection
- Need Update
- Published
- In Transaction
- Sold
- Cancelled

### Editing rule

- `Pending Inspection`: khong duoc sua
- `Need Update`: duoc sua
- `In Transaction`: lock listing

### Reserve rule

- Chi reserve khi thanh toan thanh cong
- Cancel thi mo khoa lai

## 6) Role system

Login chon 1 role:

- Buyer
- Seller
- Inspector
- Admin

Register chi cho:

- Buyer
- Seller

## 7) Inspector dashboard can co

- Danh sach listing cho duyet
- Trang chi tiet
- 3 nut quyet dinh
- Filter theo status

## 8) Muc tieu truoc khi ra hoi dong

Phai chay duoc full flow:

Seller dang -> Inspector duyet -> Publish -> Buyer dat coc -> Sold

Khong can architecture dep, khong can pattern training.
Chi can:

- Khong sai business rule
- Khong bug auth
- Flow ro rang

## 9) Loai bo khoi pham vi

- UI UX Pro Max
- Git training docs
- Design System Generator
- Checklist anti-pattern
- Quy chuan hoc thuat nang cao
- Tai lieu on tap/training copy tu docs
