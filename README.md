import random

class SmartGuessGame:
    def __init__(self, low=1, high=100):
        self.low = low
        self.high = high
        self.secret = random.randint(low, high)
        self.history = []  # ذخیره حدس‌های قبلی

    def give_hint(self, guess):
        """راهنمایی به بازیکن بر اساس حدسش"""
        if guess < self.secret:
            return "عدد بزرگتره 📈"
        elif guess > self.secret:
            return "عدد کوچکتره 📉"
        else:
            return "درست حدس زدی 🎉"

    def play(self):
        print(f"من یه عدد بین {self.low} تا {self.high} انتخاب کردم. حدس بزن!")
        attempts = 0

        while True:
            try:
                guess = int(input("حدست: "))
            except ValueError:
                print("لطفاً فقط عدد وارد کن! 🔢")
                continue

            attempts += 1
            self.history.append(guess)
            hint = self.give_hint(guess)
            print(hint)

            if guess == self.secret:
                print(f"👏 آفرین! در {attempts} تلاش موفق شدی.")
                break

        # تحلیل هوشمندانه
        print("\n📊 تحلیل بازی:")
        print(f"حدس‌های تو: {self.history}")
        avg_guess = sum(self.history) / len(self.history)
        print(f"میانگین حدس‌هات: {avg_guess:.2f}")
        if avg_guess > self.secret:
            print("تو بیشتر سمت عددهای بزرگ رفتی!")
        else:
            print("تو بیشتر سمت عددهای کوچیک رفتی!")

if __name__ == "__main__":
    game = SmartGuessGame()
    game.play()
