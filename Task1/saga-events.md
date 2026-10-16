# Реестр событий Saga оформления заказа

| Этап | Тип события | Название | Издатель | Потребители |
| --- | --- | --- | --- | --- |
| Заказ принят | domain | OrderCreated | Order Service | Catalog Service |
| Цены и позиции проверены | domain | OrderValidated | Catalog Service | Inventory Service, Order Service |
| Цена изменилась или товар удален | failure | OrderValidationFailed | Catalog Service | Order Service |
| Все позиции зарезервированы | domain | StockReserved | Inventory Service | Payment Service, Order Service |
| Недостаточно товара | failure | StockReservationFailed | Inventory Service | Order Service |
| Создана ссылка для оплаты | domain | PaymentReady | Payment Service | Order Service |
| Списание подтверждено | domain | PaymentSucceeded | Payment Service | Delivery Service, Order Service |
| Оплата отклонена или срок истек без списания | failure | PaymentFailed | Payment Service | Inventory Service, Order Service |
| Заявка на доставку подтверждена | domain | DeliveryCreated | Delivery Service | Order Service |
| Окончательный отказ создания доставки | failure | DeliveryCreationFailed | Delivery Service | Payment Service, Order Service |
| Деньги возвращены | compensation | RefundSucceeded | Payment Service | Inventory Service, Order Service |
| Резерв освобожден | compensation | StockReleased | Inventory Service | Order Service |
| Оформление завершено | domain | OrderConfirmed | Order Service | Notification Service |
| Отмена завершена | compensation | OrderCancelled | Order Service | Notification Service |

Отмена после оплаты завершается только после возврата денег и снятия резерва. При ошибке цены или отсутствии товара компенсации не нужны.
