# project-python
עבודה סוף סמסטר טל לביא 211426168 ואיתי אביאני 209522721
                                                                                                                                # הגדרת מחרוזות עם שמות וקודים של בעלי חיים
txt1 = "Dog12, CAT3, LiOn7, DolphiN11, fish6"
txt2 = "PIG17, bear29, BiRd8"
txt3 = "SNAKE39, donkey14"

                                                                                                                            # יצירת מילון ריק לאחסון שמות וקודים של בעלי חיים
animals = {}

                                                                                                                          # עיבוד כל אחת מהמחרוזות והכנסת הנתונים לתוך המילון
for txt in [txt1, txt2, txt3]:
    for animal in txt.split(', '):
                                                                                                        # הפרדת השם מהמספר והכנסתם למילון תוך תיקון האותיות לאות גדולה בתחילת השם
        name, code = ''.join([i for i in animal if not i.isdigit()]).strip().lower(), ''.join([i for i in animal if i.isdigit()])
        animals[int(code)] = name.capitalize()

                                                                                                                                  #  פונקציה לבדיקה האם קלט הוא מספר חוקי
def is_valid_number(input_str):
    try:
        int(input_str)
        return True
    except ValueError:
        return False
    
                                                                                                                                      # פונקציה לקבלת מספר חוקי מהמשתמש
def get_valid_number(prompt):
    while True:
        input_str = input(prompt)
        if is_valid_number(input_str):
            return int(input_str)
        else:
            print("Invalid input, please enter a number.")

                                                                                                                  # הצגת תפריט המשתמש הראשי והפעלת פונקציות לפי בחירת המשתמש
def main_menu():
    while True:
        print("\nWelcome to the Zoo Information System,")
        print("Please choose an option:")
        print("[1] - Search animal by code")
        print("[2] - Search animal by name")
        print("[3] - Add a new animal")
        print("[4] - Remove an animal from the database")
        print("[5] - Exit")
        choice = input("Your choice: ")
        if choice == '1':
            search_by_code()
        elif choice == '2':
            search_by_name()
        elif choice == '3':
            add_animal()
        elif choice == '4':
            delete_animal()
        elif choice == '5':
            print("Thank you and goodbye!")
            break
        else:
            print("Invalid choice, please try again.")

                                                                                                                                                # חיפוש בעל חיים לפי קוד
def search_by_code():
    code = get_valid_number("Please enter a code: ")
    animal = animals.get(code, None)
    if animal:
        print(f"Animal code: {code}\nAnimal name: {animal}")
    else:
        print("No animal found with the given code.")

                                                                                                                                                # חיפוש בעל חיים לפי שם
def search_by_name():
    search_term = input("Please enter a name to search for: ").strip()
    if not search_term.isalpha():
        print("Invalid input, please enter letters only.")
        return
    found = False
    for code, name in animals.items():
        if search_term.lower() in name.lower():
            if not found:
                print("Animals found:")
                found = True
            print(f"Animal code: {code}\nAnimal name: {name}")
    if not found:
        print("No matching animals found.")

                                                                                                                                            # הוספת בעל חיים חדש למאגר
def add_animal():
    code = get_valid_number("Please enter an animal code: ")
    if code in animals:
        print("Error: Animal code already exists.")
    else:
        name = input("Please enter an animal name: ")
        if not name.isalpha():
            print("Invalid animal name, please enter letters only.")
            return
        animals[code] = name.capitalize()
        print("Animal added successfully.")

                                                                                                                                                # מחיקת בעל חיים מהמאגר
def delete_animal():
    code = get_valid_number("Please enter an animal code: ")
    if code in animals:
        del animals[code]
        print("Animal removed successfully.")
    else:
        print("Error: No animal found with the given code.")

                                                                                                                        # הרצת תפריט המשתמש הראשי אם הסקריפט הופעל ישירות
if __name__ == "__main__":
    main_menu()


