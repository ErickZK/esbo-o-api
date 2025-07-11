# 📦 Integração API Moto Táxi - AtendeLoja

Documentação da API REST do sistema Moto Táxi para uso com AtendeLoja.

---

## 🌐 URL Base

https://meumototaxi.com.br

---

## 🔐 Headers Padrão

Authorization: Bearer {token}   
Content-Type: application/json

---

# 🚚 Endpoints, Body e Respostas

---

## 1️⃣ Estimar Entrega

Endpoint:
POST /v1/deliveries/estimate

### 📨 Body (Request)

```json
{
  "pickup": {
    "address": "Rua da Loja, 123, Cidade, Estado",
    "contact": {
      "first_name": "Loja",
      "last_name": "AtendeLoja",
      "phone": "+5511999999999",
      "email": "loja@exemplo.com"
    }
  },
  "dropoff": {
    "address": "Rua do Cliente, 999, Cidade, Estado",
    "contact": {
      "first_name": "Cliente",
      "last_name": "Souza",
      "phone": "+5511988888888",
      "email": "cliente@exemplo.com"
    }
  },
  "manifest": {
    "reference_id": "pedido-12345",
    "description": "Descrição dos itens"
  }
}
```

# ✅ Resposta (Response)

```json
{
  "estimate_id": "est123456",
  "currency": "BRL",
  "price": 18.50,
  "distance_meters": 4200,
  "duration_minutes": 20,
  "expires_at": "2025-07-10T14:30:00Z"
}
```

# 2️⃣ Criar Entrega

```
POST /v1/deliveries
```

# 📨 Body

```json
{
  "pickup": { ... },
  "dropoff": { ... },
  "manifest": { ... }
}
```

# ✅ Resposta

```json
{
  "delivery_id": "del123456",
  "status": "delivery_created",
  "tracking_url": "https://meumototaxi.com.br/track/del123456",
  "price": 18.50,
  "created_at": "2025-07-10T14:05:00Z"
}
```

## 3️⃣ Consultar Status da Entrega

Endpoint:

```
bashCopiarEditarGET /v1/deliveries/{delivery_id}
```

### 📨 Body

(não requer body)

### ✅ Resposta

```json
{
  "delivery_id": "del123456",
  "status": "pickup_in_progress",
  "pickup_eta_minutes": 5,
  "dropoff_eta_minutes": 20,
  "current_location": {
    "lat": -19.4670,
    "lng": -42.5330
  },
  "courier": {
    "name": "João",
    "phone": "+5511999999999",
    "vehicle": "Moto"
  },
  "tracking_url": "https://meumototaxi.com.br/track/del123456"
}
```

---

## 4️⃣ Cancelar Entrega

Endpoint:

```
POST /v1/deliveries/{delivery_id}/cancel
```

### 📨 Body

(não requer body)

### ✅ Resposta

```json
{
  "delivery_id": "del123456",
  "status": "cancelled",
  "cancelled_at": "2025-07-10T14:10:00Z"
}
```

---

## 5️⃣ Atualizar Entrega

Endpoint:

```json
PATCH /v1/deliveries/{delivery_id}
```

### 📨 Body (Exemplo de atualização de contato)

```json
{
  "dropoff": {
    "contact": {
      "first_name": "NovoNome",
      "last_name": "Cliente",
      "phone": "+5511999999999",
      "email": "novoemail@exemplo.com"
    }
  }
}
```

### ✅ Resposta

```json
{
  "delivery_id": "del123456",
  "status": "delivery_created",
  "updated_at": "2025-07-10T14:12:00Z"
}
```

# 🧭 Status Possíveis da Entrega

- quote_created
- delivery_created
- courier_assigned
- pickup_in_progress
- picked_up
- dropoff_in_progress
- delivered
- cancelled

---

# 📌 Observações

- Todas as requisições devem conter Bearer Token no header.
