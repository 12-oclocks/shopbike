# SHOPBIKE - HANDOVER CORE VERSION

> Scope: chi giu lai phan cot loi de code dung business flow ShopBike.
> Khong ap dung training materials, UI/UX "pro max", hoac guideline hoc thuat nang cao.

## 1. Project Nature

ShopBike la marketplace mua ban xe dap cu co kiem dinh.

Flow chinh:

1. Seller tao listing
2. Inspector kiem dinh va ra quyet dinh
3. Listing du dieu kien thi publish
4. Buyer dat coc / giao dich
5. Listing chuyen trang thai Sold

## 2. Tech Stack Dang Dung

- React + TypeScript
- React Router v6
- Zustand
- Axios
- Tailwind
- Backend REST API (`/api/...`)

Khong rang buoc pattern phuc tap. Uu tien UI ro rang, de dung, chay dung flow.

## 3. Authentication (Practical)

- Zustand luu `accessToken`
- Co `RequireAuth`
- Co `GuestGuard`
- Logout phai clear token

Khong bat buoc tuan thu guideline auth phuc tap, chi can on dinh va dung.

## 4. API Layer

- Co `apiClient`
- Interceptor tu dong attach token
- Refresh token la tuy chon (khuyen nghi neu can)
- Component nen goi qua service layer

Khong can architecture qua cung, nhung phai de bao tri.

## 5. Business Logic Core (Khong duoc sai)

### Publish Rule

Listing chi duoc Published khi Inspector `APPROVE`.

### Inspection Decision

Inspector co 3 ket qua:

- `APPROVE` -> Publish
- `REJECT` -> Ket thuc listing
- `NEED_UPDATE` -> Tra ve Seller de sua

### Listing States

- `Draft`
- `Pending Inspection`
- `Need Update`
- `Published`
- `In Transaction`
- `Sold`
- `Cancelled`

### Editing Rule

- `Pending Inspection` -> Khong duoc sua
- `Need Update` -> Duoc sua
- `In Transaction` -> Lock listing

### Reserve Rule

- Chi reserve khi thanh toan thanh cong
- Neu cancel giao dich thi mo khoa listing

## 6. Role System

Role khi login:

- Buyer
- Seller
- Inspector
- Admin

Role khi register:

- Buyer
- Seller

## 7. Inspector Dashboard Bat Buoc Co

- Danh sach listing cho duyet
- Trang chi tiet listing
- 3 nut quyet dinh (`APPROVE`, `REJECT`, `NEED_UPDATE`)
- Filter theo status

## 8. Muc tieu truoc khi demo / bao ve

Phai chay duoc full flow:

Seller dang -> Inspector duyet -> Publish -> Buyer dat coc -> Sold

Uu tien:

1. Khong sai business rule
2. Khong bug auth
3. Flow ro rang, co the trinh bay

## 9. Explicitly Out of Scope

Khong uu tien / khong bat buoc:

- UI/UX Pro Max skill set
- Git training docs
- Design system generator
- Checklist anti-pattern hoc thuat
- Bo tai lieu on luyen nang cao

Neu co xung dot giua tai lieu khac va file nay, uu tien file nay cho quyet dinh implementation.
