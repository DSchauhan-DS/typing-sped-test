import random
import time
import tkinter as tk
from tkinter import messagebox

PASSAGES = [
    "Python makes it easier to turn creative ideas into useful programs.",
    "Small daily practice can improve your focus, confidence, and typing speed.",
    "Technology is most powerful when it helps solve everyday problems.",
    "Learning to code is a journey built one clear step at a time.",
    "A calm mind and steady hands can make typing both fast and accurate."
]

TEST_SECONDS = 30


class TypingSpeedTest:
    def __init__(self, root):
        self.root = root
        self.root.title("⚡ TypeSprint — Typing Speed Test")
        self.root.geometry("760x560")
        self.root.configure(bg="#101827")

        self.started = False
        self.finished = False
        self.start_time = None
        self.remaining = TEST_SECONDS
        self.target = random.choice(PASSAGES)

        tk.Label(
            root, text="⚡ TypeSprint", font=("Arial", 28, "bold"),
            fg="#67e8f9", bg="#101827"
        ).pack(pady=(22, 4))

        tk.Label(
            root, text="Test your speed. Chase your best.",
            font=("Arial", 12), fg="#a8b3c7", bg="#101827"
        ).pack(pady=(0, 18))

        self.timer_label = tk.Label(
            root, text=f"⏱  {TEST_SECONDS}", font=("Arial", 20, "bold"),
            fg="#facc15", bg="#101827"
        )
        self.timer_label.pack(pady=6)

        self.passage_label = tk.Label(
            root, text=self.target, wraplength=660, justify="left",
            font=("Arial", 16), fg="#e5e7eb", bg="#1e293b",
            padx=20, pady=20
        )
        self.passage_label.pack(fill="x", padx=40, pady=14)

        self.text_box = tk.Text(
            root, height=7, wrap="word", font=("Arial", 14),
            bg="#0b1220", fg="white", insertbackground="white",
            padx=12, pady=12, relief="flat"
        )
        self.text_box.pack(fill="x", padx=40, pady=8)
        self.text_box.bind("<KeyRelease>", self.on_type)

        self.text_box.tag_configure("correct", foreground="#4ade80")
        self.text_box.tag_configure("wrong", foreground="#fb7185")

        self.stats_label = tk.Label(
            root, text="WPM: —       Accuracy: —",
            font=("Arial", 15, "bold"), fg="#cbd5e1", bg="#101827"
        )
        self.stats_label.pack(pady=12)

        self.status_label = tk.Label(
            root, text="Start typing to begin the timer.",
            font=("Arial", 11), fg="#94a3b8", bg="#101827"
        )
        self.status_label.pack()

        self.restart_button = tk.Button(
            root, text="↻  New Test", command=self.restart,
            font=("Arial", 12, "bold"), bg="#0891b2", fg="white",
            activebackground="#0e7490", activeforeground="white",
            relief="flat", padx=18, pady=9, cursor="hand2"
        )
        self.restart_button.pack(pady=16)

    def on_type(self, _event=None):
        if self.finished:
            return

        if not self.started and self.text_box.get("1.0", "end-1c"):
            self.started = True
            self.start_time = time.time()
            self.tick()

        typed = self.text_box.get("1.0", "end-1c")
        self.show_feedback(typed)

        elapsed = max(time.time() - self.start_time, 0.1) if self.start_time else 0.1
        words = len(typed.split())
        wpm = words / elapsed * 60
        correct = sum(
            1 for i, char in enumerate(typed)
            if i < len(self.target) and char == self.target[i]
        )
        accuracy = correct / len(typed) * 100 if typed else 100
        self.stats_label.config(
            text=f"WPM: {wpm:.0f}       Accuracy: {accuracy:.0f}%"
        )

        if typed == self.target:
            self.finish_test("Passage completed! Amazing typing!")

    def show_feedback(self, typed):
        self.text_box.tag_remove("correct", "1.0", "end")
        self.text_box.tag_remove("wrong", "1.0", "end")

        for i, char in enumerate(typed):
            start = f"1.0+{i}c"
            end = f"1.0+{i + 1}c"
            tag = "correct" if i < len(self.target) and char == self.target[i] else "wrong"
            self.text_box.tag_add(tag, start, end)

    def tick(self):
        if self.finished:
            return

        elapsed = time.time() - self.start_time
        self.remaining = max(0, TEST_SECONDS - int(elapsed))
        self.timer_label.config(text=f"⏱  {self.remaining}")

        if self.remaining <= 0:
            self.finish_test("Time is up!")
        else:
            self.root.after(200, self.tick)

    def finish_test(self, message):
        if self.finished:
            return

        self.finished = True
        self.text_box.config(state="disabled")

        typed = self.text_box.get("1.0", "end-1c")
        elapsed = max(time.time() - self.start_time, 0.1)
        words = len(typed.split())
        wpm = words / elapsed * 60
        correct = sum(
            1 for i, char in enumerate(typed)
            if i < len(self.target) and char == self.target[i]
        )
        accuracy = correct / len(typed) * 100 if typed else 0

        if wpm >= 60:
            rating = "Speed legend!"
        elif wpm >= 40:
            rating = "Great job!"
        elif wpm >= 25:
            rating = "Good work!"
        else:
            rating = "Keep practicing!"

        self.status_label.config(text=rating)
        messagebox.showinfo(
            "Test complete",
            f"{message}\n\nSpeed: {wpm:.1f} WPM\nAccuracy: {accuracy:.1f}%\n\n{rating}"
        )

    def restart(self):
        self.target = random.choice(PASSAGES)
        self.started = False
        self.finished = False
        self.start_time = None
        self.remaining = TEST_SECONDS

        self.passage_label.config(text=self.target)
        self.timer_label.config(text=f"⏱  {TEST_SECONDS}")
        self.stats_label.config(text="WPM: —       Accuracy: —")
        self.status_label.config(text="Start typing to begin the timer.")

        self.text_box.config(state="normal")
        self.text_box.delete("1.0", "end")
        self.text_box.focus_set()


root = tk.Tk()
app = TypingSpeedTest(root)
root.mainloop()

