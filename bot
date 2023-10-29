def input_error(func):
    def inner(*args, **kwargs):
        try:
            return func(*args, **kwargs)
        except ValueError:
            return "Give me name and phone please."
        except KeyError:
            return "This contact does not exist."
        except IndexError:
            return "The command was not recognized or the parameters are incorrect."

    return inner


@input_error
def add_contact(args, contacts):
    name, phone = args
    contacts[name] = phone
    return "Contact added."


@input_error
def delete_contact(args, contacts):
    name = args[0]
    del contacts[name]
    return "Contact deleted."


@input_error
def get_contact(args, contacts):
    name = args[0]
    phone = contacts[name]
    return f"{name}'s phone is {phone}"


@input_error
def list_contacts(args, contacts):
    return "\n".join([f"{name}: {phone}" for name, phone in contacts.items()])


# Sample usage:


def main():
    contacts = {}
    while True:
        user_input = (
            input("Enter command (add, delete, list, get, exit): ").strip().split()
        )
        cmd = user_input[0]
        args = user_input[1:]
        if cmd == "add":
            print(add_contact(args, contacts))
        elif cmd == "delete":
            print(delete_contact(args, contacts))
        elif cmd == "list":
            print(list_contacts(args, contacts))
        elif cmd == "get":
            print(get_contact(args, contacts))
        elif cmd == "exit":
            break
        else:
            print("Unknown command. Try again.")


if __name__ == "__main__":
    main()
