import random

class Product:
    def __init__(self, name, price, quantity):
        self.name = name
        self.price = price
        self.quantity = quantity
    def total_value(self):
        return self.price * self.quantity

class PerishableProduct(Product):
    def __init__(self, name, price, quantity, expiry_days):
        super().__init__(name, price, quantity)
        self.expiry_days = expiry_days
    def total_value(self):
        value = super().total_value()
        if self.expiry_days < 5:
            value *= 0.8
        return value

class InventoryManager:
    def __init__(self):
        self.products = []
    def add_product(self, product):
        self.products.append(product)
    def list_inventory(self):
        for i, p in enumerate(self.products, 1):
            print(f"{i}. {p.name} → Qty: {p.quantity}, Value: {p.total_value()}")
    def search_by_name(self, term):
        for p in self.products:
            if term.lower() in p.name.lower():
                print(f"{p.name} → Qty: {p.quantity}, Value: {p.total_value()}")
    def restock_all(self):
        for p in self.products:
            p.quantity += random.randint(1, 5)

manager = InventoryManager()
manager.add_product(Product("Apple", 5, 10))
manager.add_product(PerishableProduct("Milk", 4, 5, 3))

print("Inventory:")
manager.list_inventory()

print("\nSearch 'milk':")
manager.search_by_name("milk")

manager.restock_all()

print("\nAfter restocking:")
manager.list_inventory()
