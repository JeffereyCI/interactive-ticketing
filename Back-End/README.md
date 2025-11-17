# Interactive Ticketing - Backend API

Backend API untuk sistem antrian rumah sakit menggunakan Golang.

## Fitur

- ✅ CRUD Data Pasien
- ✅ Generate Nomor Antrian Otomatis
- ✅ Manajemen Status Antrian
- ✅ Statistik Antrian
- ✅ Filter Pasien per Loket
- ✅ Penyimpanan Data dengan JSON
- ✅ CORS Support untuk Frontend

## Teknologi

- Go 1.21+
- Gorilla Mux (Router)
- CORS Middleware

## Instalasi

1. Install dependencies:
```bash
go mod download
```

2. Jalankan server:
```bash
go run main.go
```

Server akan berjalan di `http://localhost:8080`

## API Endpoints

### 1. Get All Patients
```
GET /api/patients
```
Response:
```json
[
  {
    "id": "P1234567890",
    "queueNumber": "A-001",
    "fullName": "John Doe",
    "nik": "1234567890123456",
    "email": "john@email.com",
    "phone": "08123456789",
    "dateOfBirth": "1990-01-01",
    "address": "Jakarta",
    "specialist": "Poli Umum",
    "doctor": "Dr. Smith",
    "complaint": "Demam",
    "status": "waiting",
    "loketNumber": "1",
    "createdAt": "2025-11-15T10:00:00Z"
  }
]
```

### 2. Create Patient
```
POST /api/patients
```
Request Body:
```json
{
  "fullName": "John Doe",
  "nik": "1234567890123456",
  "email": "john@email.com",
  "phone": "08123456789",
  "dateOfBirth": "1990-01-01",
  "address": "Jakarta",
  "specialist": "Poli Umum",
  "doctor": "Dr. Smith",
  "complaint": "Demam"
}
```

### 3. Get Patient by ID
```
GET /api/patients/{id}
```

### 4. Check Active Queue by Name
```
GET /api/patients/check/{name}
```
Check if patient has active queue (status: waiting or called).
Returns patient data if active queue exists, otherwise 404.

### 5. Update Patient Status
```
PUT /api/patients/{id}/status
```
Request Body:
```json
{
  "status": "called"
}
```
Status options: `waiting`, `called`, `completed`

### 6. Get Patients by Loket
```
GET /api/patients/loket/{loket}
```
Example: `/api/patients/loket/1`

### 7. Get Next Queue for Loket
```
GET /api/patients/loket/{loket}/next
```

### 8. Get Queue Statistics
```
GET /api/stats
```
Response:
```json
{
  "total": 100,
  "waiting": 50,
  "completed": 40,
  "called": 10
}
```

### 9. Reset All Data
```
POST /api/reset
```

## Mapping Loket & Specialist

- **Loket 1**: Poli Umum (Queue: A-xxx)
- **Loket 2**: Poli Gigi (Queue: B-xxx)
- **Loket 3**: Poli Anak (Queue: C-xxx)
- **Loket 4**: Poli Kandungan (Queue: D-xxx)

## Data Storage

Data disimpan dalam file `patients.json` secara otomatis setiap ada perubahan.
