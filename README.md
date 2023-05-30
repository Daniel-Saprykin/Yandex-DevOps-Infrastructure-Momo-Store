# Momo Store aka Пельменная №2

<img width="900" alt="image" src="https://user-images.githubusercontent.com/9394918/167876466-2c530828-d658-4efe-9064-825626cc6db5.png">

## Ссылки на магазин
- Кластер: http://pelmeshki-one-love.ru
- vm docker: http://158.160.25.4:8000/catalog

##### Gitlab repositories  <br>
- momo-store - [momo-store](https://gitlab.praktikum-services.ru/std-012-029/momo-store)
- momo-store-local - [momo-store-local](https://gitlab.praktikum-services.ru/std-012-029/momo-store-local) (реализован полный цыкл ci/cd)
- momo-store-Infrastructure - [momo-infra](https://gitlab.praktikum-services.ru/std-012-029/momo-store-infrastructure)

# Установка приложения локально
---
### Frontend
```bash
npm install
NODE_ENV=production VUE_APP_API_URL=http://localhost:8081 npm run serve
```
### Backend

```bash
go run ./cmd/api
go test -v ./... 
```

# Установка приложения в докере
---

Запуск магазина в докере
```sh
git git@gitlab.praktikum-services.ru:std-012-029/momo-store-local.git
cd momo-store-local
docker-compose up -d
```
open http://localhost:8000

# Infrastructure  <br>       
--- 
```sh
git clone git@gitlab.praktikum-services.ru:std-012-029/momo-store-infrastructure.git
cd momo-store-infrastructure

```

Развертывание кластера через terraform
```
export YC_TOKEN=`yc iam create-token`
cd terraform/k8s-cluster
terraform apply main.tf  -var "yc_token=${YC_TOKEN}"
```

Развертывание магазина в кластере
```
cd kubernetes
kubectl apply -f backend
kubectl apply -f frontend
```