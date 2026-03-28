# 🐾 Hướng Dẫn Cài Đặt & Chạy Dự Án UME Pet Salon

## Yêu Cầu Hệ Thống

| Phần mềm | Phiên bản tối thiểu | Link tải |
|-----------|---------------------|----------|
| Node.js | 18.x trở lên | https://nodejs.org/ |
| MongoDB | 6.x trở lên | https://www.mongodb.com/try/download/community |
| Git | 2.x | https://git-scm.com/ |

> **Lưu ý:** MongoDB phải đang chạy trước khi khởi động backend.

---

## 1. Clone dự án

```bash
git clone https://github.com/<username>/WepthucungV2.git
cd WepthucungV2
```

---

## 2. Cài đặt Backend

```bash
cd ume-backend
npm install
```

### Tạo file `.env`

Tạo file `ume-backend/.env` với nội dung:

```env
# Server
PORT=5000
NODE_ENV=development

# MongoDB
MONGODB_URI=mongodb://localhost:27017/umepetsalon

# JWT
JWT_SECRET=ume-pet-salon-secret-key-2024
JWT_REFRESH_SECRET=ume-pet-salon-refresh-secret-2024
JWT_EXPIRES_IN=1d
JWT_REFRESH_EXPIRES_IN=7d

# Google OAuth (để trống nếu không dùng)
GOOGLE_CLIENT_ID=
GOOGLE_CLIENT_SECRET=

# Frontend URL
FRONTEND_URL=http://localhost:5173

# Upload directory
UPLOAD_DIR=uploads
```

### Tạo dữ liệu mẫu

```bash
npm run seed
```

Sau khi seed xong sẽ có tài khoản:
- **Admin:** `admin@ume.com` / `Admin@123`
- **Khách hàng:** `nguyenvana@gmail.com` / `User@123` (và 7 tài khoản khác)

### Khởi động Backend

```bash
npm run dev
```

Backend sẽ chạy tại: **http://localhost:5000**

---

## 3. Cài đặt Frontend

Mở terminal mới:

```bash
cd ume-react
npm install
npm run dev
```

Frontend sẽ chạy tại: **http://localhost:5173**

---

## 4. AI Detection (Tùy chọn)

Tính năng nhận diện thú cưng cần file model ONNX:

```
ume-backend/
  models/
    yolo26n.onnx          ← Phát hiện động vật (bắt buộc)
    efficientnet_b0.onnx  ← Nhận diện giống (tùy chọn)
```

- Nếu **có** `yolo26n.onnx`: AI phát hiện + đếm động vật hoạt động
- Nếu **có thêm** `efficientnet_b0.onnx`: Nhận diện giống chó/mèo hoạt động
- Nếu **thiếu cả hai**: Trang AI Nhận diện sẽ báo lỗi (các tính năng khác vẫn hoạt động bình thường)

Tạo thư mục nếu chưa có:

```bash
mkdir ume-backend/models
```

Copy file `.onnx` vào thư mục trên.

---

## 5. Truy cập hệ thống

| Trang | URL |
|-------|-----|
| Trang chủ | http://localhost:5173 |
| Dịch vụ thú cưng | http://localhost:5173/services |
| Sản phẩm | http://localhost:5173/products |
| Thú cưng | http://localhost:5173/pets |
| AI Nhận diện | http://localhost:5173/ai-detection |
| Đặt lịch | http://localhost:5173/booking |
| Admin Dashboard | http://localhost:5173/admin |
| API Health Check | http://localhost:5000/api/health |

---

## 6. Cấu trúc dự án

```
WepthucungV2/
├── ume-backend/          # Backend Node.js + Express + MongoDB
│   ├── src/
│   │   ├── server.js     # Entry point
│   │   ├── controllers/  # Xử lý logic API
│   │   ├── models/       # MongoDB schemas
│   │   ├── routes/       # Định tuyến API
│   │   ├── middleware/    # Auth, upload, validate
│   │   ├── services/     # AI detection service
│   │   └── sockets/      # Socket.IO realtime
│   └── models/           # ONNX model files (AI)
├── ume-react/            # Frontend React 19 + TypeScript + Vite
│   ├── src/
│   │   ├── pages/        # Các trang (admin, auth, booking...)
│   │   ├── components/   # Component dùng chung
│   │   ├── services/     # API calls
│   │   ├── contexts/     # Auth, Cart context
│   │   └── styles/       # SCSS styles
│   └── public/           # Static assets
└── docs/                 # Tài liệu dự án
```

---

## 7. Các lệnh thường dùng

| Lệnh | Mô tả |
|-------|-------|
| `cd ume-backend && npm run dev` | Chạy backend (dev mode, auto-reload) |
| `cd ume-backend && npm start` | Chạy backend (production) |
| `cd ume-backend && npm run seed` | Tạo dữ liệu mẫu |
| `cd ume-react && npm run dev` | Chạy frontend (dev mode) |
| `cd ume-react && npm run build` | Build frontend cho production |

---

## 8. Xử lý lỗi thường gặp

### MongoDB chưa chạy
```
MongoServerSelectionError: connect ECONNREFUSED 127.0.0.1:27017
```
→ Khởi động MongoDB service: `mongod` hoặc mở MongoDB Compass

### Port đã bị chiếm
```
Error: listen EADDRINUSE :::5000
```
→ Đổi PORT trong file `.env` hoặc tắt process đang dùng port đó

### Thiếu dependencies
```
Cannot find module 'xxx'
```
→ Chạy lại `npm install` trong thư mục tương ứng

### AI model not found
```
Model not found: .../models/yolo26n.onnx
```
→ Copy file `yolo26n.onnx` vào `ume-backend/models/`

---

## Công nghệ sử dụng

- **Frontend:** React 19, TypeScript, Vite, SCSS, React Router v7
- **Backend:** Node.js, Express.js, MongoDB, Mongoose
- **Realtime:** Socket.IO
- **AI:** ONNX Runtime (YOLO26n + EfficientNet-B0)
- **Auth:** JWT, Google OAuth 2.0
