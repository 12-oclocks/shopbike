# SHOPBIKE - HANDOVER CORE (NO TRAINING)

Tai lieu nay chi giu phan cot loi de implement du an ShopBike.
Loai bo toan bo noi dung training, guideline hoc thuat, va UI/UX "pro max".

## 1) Ban chat du an

ShopBike la marketplace mua ban xe dap cu co kiem dinh.

Flow chinh:

`Seller -> Inspector -> Buyer -> Transaction -> Sold`

## 2) Stack dang dung (thuc te)

- React + TypeScript
- React Router v6
- Zustand
- Axios
- Tailwind
- Backend REST API `/api/...`

## 3) Auth (muc co ban, chay dung)

- Luu `accessToken` bang Zustand
- Co `RequireAuth`
- Co `GuestGuard`
- Logout phai clear token

## 4) API layer

- Co `apiClient`
- Interceptor attach token
- Refresh token neu can
- Component nen goi qua service layer

## 5) Business logic cot loi (khong duoc sai)

### Publish rule

Listing chi duoc `Published` khi Inspector `APPROVE`.

### Inspection decisions

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

- Pending Inspection -> khong duoc sua
- Need Update -> duoc sua
- In Transaction -> lock listing

### Reserve rule

- Chi reserve khi thanh toan thanh cong
- Cancel thi mo khoa lai listing

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

## 8) Muc tieu truoc hoi dong/demo

Phai chay full flow:

`Seller dang -> Inspector duyet -> Publish -> Buyer dat coc -> Sold`

Uu tien:

- Dung business rule
- Auth on dinh
- Flow ro rang

## Out of scope

Khong uu tien:

- UI UX Pro Max
- Git training docs
- Design system generator
- Checklist anti-pattern
- Quy chuan hoc thuat nang cao
