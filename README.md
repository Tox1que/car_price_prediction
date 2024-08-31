# Определение стоимости автомобилей  

### Описание проекта  
Сервис по продаже автомобилей с пробегом «Не бит, не крашен» разрабатывает приложение для привлечения новых клиентов. В нём можно быстро узнать рыночную стоимость своего автомобиля. В вашем распоряжении исторические данные: технические характеристики, комплектации и цены автомобилей. Вам нужно построить модель для определения стоимости. 

Заказчику важны:

- качество предсказания;
- скорость предсказания;
- время обучения.  

### Описание данных  
**Признаки**  
`DateCrawled` — дата скачивания анкеты из базы  
`VehicleType` — тип автомобильного кузова  
`RegistrationYear` — год регистрации автомобиля  
`Gearbox` — тип коробки передач  
`Power` — мощность (л. с.)  
`Model` — модель автомобиля  
`Kilometer` — пробег (км)  
`RegistrationMonth` — месяц регистрации автомобиля  
`FuelType` — тип топлива  
`Brand` — марка автомобиля  
`Repaired` — была машина в ремонте или нет  
`DateCreated` — дата создания анкеты  
`NumberOfPictures` — количество фотографий автомобиля  
`PostalCode` — почтовый индекс владельца анкеты (пользователя)  
`LastSeen` — дата последней активности пользователя  
**Целевой признак**  
`Price` — цена (евро)  

### Ход исследования:  
- приведены типы данных;  
- удалены неинформативные признаки;  
- в столбцах `price`, `registration_year`, `brand` и `power` удалены аномалии и выбросы;
- пропуски:
    - `vehicle_type`, `model` - удалены;
    - `power` - заполнены с учётом марки автомобиля, модели и коробки передач;
    - `gearbox` - заполнены значением `manual`;
    - `repaired` - выделены в отдельную группу;
    - `fuel_type` - заполнены с помощью модели случайного леса;  
- после предобработки сохранилось примерно 82% от изначального объёма данных;  
- набор данных разделён на обучающую и тестовую выборки в соотношении 4:1;  
- произведено сравнение моделей линейной регрессии и градиентного бустинга на кросс-валидации;  
- модель градиентного бустинга превзошла линейную регрессию как по точности предсказаний (критерий качества - `RMSE`), так и по скорости обучения.  

Рассмотренные в ходе исследования модели предсказывали стоимость транспортного средства, зарегистрированного не ранее 1990-го года, мощностью от 40 до 450 л. с.  