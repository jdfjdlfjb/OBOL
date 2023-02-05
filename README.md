# OBOL

# Встановлення та реєстрація кластера OBOL

## Рекомендовані вимоги для сервера
16GB RAM 1TB дискового простору 4Cores CPU



### Оновлюємо наш сервер
```
sudo apt update && sudo apt upgrade -y
```

### Встановлюємо docker
```
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh 
```

### І docker-compose
```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

### Далі копіюємо дистрибутив проекту
```
git clone https://github.com/ObolNetwork/charon-distributed-validator-node.git
```

### Надаємо права і переходимо в папку проекту
```
chmod o+w charon-distributed-validator-node
cd charon-distributed-validator-node
```

### Створюємо приватний ключ ENR
```
docker run --rm -v "$(pwd):/opt/charon" obolnetwork/charon:v0.13.0 create enr
```

### Показано буде приблизно так
```
Created ENR private key: .charon/charon-enr-private-key
enr:-JG4QGQpV4qYe32QFUAbY1UyGNtNcrVMip83cvJRhw1brMslPeyELIz3q6dsZ7GblVaCjL_8FKQhF6Syg-O_kIWztimGAYHY5EvPgmlkgnY0gmlwhH8AAAGJc2VjcDI1NmsxoQKzMe_GFPpSqtnYl-mJr8uZAUtmkqccsAx7ojGmFy-FY4N0Y3CCDhqDdWRwgg4u
```

## Збережіть приватний ключ,він знаходиться  ~/charon-distributed-validator-node/.charon/charon-enr-private-key


## Подальші кроки виконує лідер кластера!

### Лідер кластера повинен зібрати адреси гаманців метамаска, зазначених під час реєстрації (тільки адреса, у жодному разі не надавайте сід-фрази і приват-кей від гаманця)


### Далі лідер переходить по https://bia.launchpad.obol.tech/ і підключає гаманець вказаний під час реєстрації.

![16](https://user-images.githubusercontent.com/112564909/216807287-ee353e87-1384-4a23-8866-43456b5d925a.jpg)

### Після вибирає Create a Cluster with a group і натискає Get Started!

![18](https://user-images.githubusercontent.com/112564909/216807536-5f2a5d27-9f20-491a-9259-334a5e8bec7b.jpg)

### Далі йде налаштування кластера, задається ім'я кластера, обирається кількість операторів, вводяться адреси гаманців операторів, обираємо кількість валідаторів (за кожного валідатора необхідно заплатити 32 Goerly ETH), в поле вставляємо ENR згенерований раніше, задаємо адресу для винагород, за замовчуванням адреса лідера, і натискаємо створити конфігурацію кластера.


![19](https://user-images.githubusercontent.com/112564909/216807651-5fa2cad1-f8f6-470e-b6be-11c52b727498.jpg)

### Перевіряємо параметри, підтверджуємо, і підтверджуємо через метамаск, після всіх підтверджень з'явиться групове посилання, яке потрібно відправити операторам.


![20](https://user-images.githubusercontent.com/112564909/216807716-46e79afe-1bc8-449a-95a3-2fd20ae1bc50.jpg)

## Далі відбувається реєстрація операторів і отримання ключів для проходження церемонії DKG, після реєстрації всіх операторів посилання на церемонію з'явиться і у лідера.

### Оператор переходить за посиланням, наданим лідером, і підключає гаманець, вказаний під час реєстрації

![21](https://user-images.githubusercontent.com/112564909/216807768-598630c7-68b7-4d2a-a10b-d4c607793643.jpg)

### Після перевіряє що його адреса є у вікні нижче і тисне "Get Started"

![22](https://user-images.githubusercontent.com/112564909/216807799-6d9288e3-9a5d-4853-bdb2-af4f6e95e9f0.jpg)

### Після перевіряє конфігурацію, складену лідером, вставляє свій ключ ENR і підтверджує участь

![23](https://user-images.githubusercontent.com/112564909/216807845-59ac4203-b038-4069-a5c5-55598dc076a4.jpg)

Після того як усі оператори підтвердять участь з'явиться рядок для проходження DKG

![24](https://user-images.githubusercontent.com/112564909/216807868-e5223368-1af6-4526-a14b-ab3f88f2fdbc.jpg)

 Необхідно узгодити дії та запускати разом, копіюємо рядок option 1 і запускаємо його на сервері з папки ~/charon-distributed-validator-node

Розпочнеться процедура DKG, після завершення будуть сформовані файли deposit-data.json, cluster-lock.json і папка з ключем валідатора validator_keys/ все це необхідно зберегти, найпростіше зберегти всю папку ~/charon-distributed-validator-node/.charon/.

Після процедури DKG лідер активує валідатора заплативши 32 Goerly ETH за кожного валідатора

Далі запускаємо ноду командою docker-compose up -d з папки ~/charon-distributed-validator-node

Дивимося статистику і працездатність ноди через інтерфейс 
http://your_node_ip:3000/d/singlenode/

### Після цього необхідно заповнити форму (реєстрація кластера) https://docs.google.com/forms/d/e/1FAIpQLSecM79NFZe8E0VE2FTcrHoe4qUf3_zZZ_s_YFGQo-y9EykCmg/viewform 




