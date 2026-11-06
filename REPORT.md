# Отчёт. День 4

По каждому заданию: что было не так и как ты это заметил. Одной-двумя фразами.

**Задание 1** (пустой столбец):  была ошибка в слове price, поэтому столбец с ценой не заполнялся, в строке где нужно было указать остаток была указна цена. Заметил по подсказкам.

**Задание 2 (фильтр по категории):**  программа сравнивала айди товара и айди категории, поменял p.id на p.CategoryId

**Задание 3 (поиск):** поиск шел по точечному названию, добавил  StringComparison.OrdinalIgnoreCase в contains

Задание 4 : дописал код, чтобы при нажатии галочки выходили только товары, которые есть на складе:
 if (InStockBox.IsChecked == true)
        {
            products = products.Where(p => p.Stock > 0);
        } 

Задание 5: foundtext не показывал сколько товаров найдено, заменил неизвестно на result.Count

**Задание 6 (чужой состав заказа): список товаров получали по клиент айди. заменил ClientId на Id** 

Задание 7: var itemTotal = items.Sum(i => i.Price * i.Quantity);
        TotalText.Text = $"Сумма заказа: {itemTotal} ₽";

**Задание 8 (новый товар):**  не было проверки остатка, был лишняя строка, которая указывала остаток 0, в конце не было добавлено сохранение. добавил проверку:   if (!int.TryParse(StockBox.Text, out int stock))
        {
            ShowMessage("Остаток должен быть числом");
            return;
стер лишнюю строку, в конце добавил await LoadProducts();

задание 9:  private async void SetStatus_Click(object? sender, RoutedEventArgs e)
    {
        var order = OrdersGrid.SelectedItem as Order;
        if (order == null)
        {
            ShowMessage("Выбери заказ");
            return;
        }

        var status = StatusBox.SelectedItem as string;
        if (status == null)
        {
            ShowMessage("Выбери статус");
            return;
        }

        var error = await Api.SetStatus(order.Id, status);
        if (error != null)
        {
            ShowMessage(error);
            return;
        }

        ShowMessage($"Статус заказа {order.Id} изменён на «{status}»");

        await LoadOrders();
    }
**Что было самым сложным:** задание 9, сделал по примеру 8.
