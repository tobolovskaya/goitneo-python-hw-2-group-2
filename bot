import re


class Field:
    def __init__(self, value):
        self.value = value

    def __str__(self):
        return str(self.value)


class Name(Field):
    def __init__(self, name):
        super().__init__(name)


class Phone(Field):
    PHONE_REGEX = re.compile(r"^\d{10}$")

    def __init__(self, phone):
        if not self.PHONE_REGEX.match(phone):
            raise ValueError("Invalid phone format. Expected format: 10 digits.")
        super().__init__(phone)


class Record:
    def __init__(self, name):
        self.name = Name(name)
        self.phones = []

    def add_phone(self, phone):
        self.phones.append(Phone(phone))

    def remove_phone(self, phone):
        phone_obj = Phone(phone)
        if phone_obj in self.phones:
            self.phones.remove(phone_obj)

    def edit_phone(self, old_phone, new_phone):
        phone_obj = Phone(old_phone)
        if phone_obj in self.phones:
            index = self.phones.index(phone_obj)
            self.phones[index] = Phone(new_phone)

    def find_phone(self, phone):
        phone_obj = Phone(phone)
        return phone_obj if phone_obj in self.phones else None

    def __str__(self):
        phones = "; ".join(map(str, self.phones))
        return f"Contact name: {self.name}, phones: {phones}"


class AddressBook:
    def __init__(self):
        self.data = {}

    def add_record(self, record):
        self.data[record.name.value] = record

    def find(self, name):
        return self.data.get(name)

    def delete(self, name):
        if name in self.data:
            del self.data[name]

    def __str__(self):
        return "\n".join(map(str, self.data.values()))


# Sample usage:

book = AddressBook()

john_record = Record("John")
john_record.add_phone("1234567890")
john_record.add_phone("5555555555")
book.add_record(john_record)

jane_record = Record("Jane")
jane_record.add_phone("9876543210")
book.add_record(jane_record)

for name, record in book.data.items():
    print(record)

john = book.find("John")
john.edit_phone("1234567890", "1112223333")

print(john)  # Expected output: Contact name: John, phones: 1112223333; 5555555555

found_phone = john.find_phone("5555555555")
print(f"{john.name}: {found_phone}")  # Expected output: John: 5555555555

book.delete("Jane")
