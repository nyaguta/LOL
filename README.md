import numpy as np
import matplotlib.pyplot as plt
from datetime import datetime, timedelta

def circular_day_planner(events):
    plt.figure(figsize=(6, 6))
    plt.axis('off')
    plt.gca().add_patch(plt.Circle((0.5, 0.5), 0.4, color='lightgray'))

    for i, (start, end, label) in enumerate(events):
        start_time = datetime.strptime(start, "%H:%M")
        end_time = datetime.strptime(end, "%H:%M")

        start_angle = (start_time.hour % 12 + start_time.minute / 60) / 12 * 2 * np.pi
        end_angle = (end_time.hour % 12 + end_time.minute / 60) / 12 * 2 * np.pi

        plt.gca().add_patch(plt.Wedge((0.5, 0.5), 0.4, start_angle * 180 / np.pi, end_angle * 180 / np.pi, width=0.1, color='blue'))
        plt.text(0.5 + 0.35 * np.cos((start_angle + end_angle) / 2), 0.5 + 0.35 * np.sin((start_angle + end_angle) / 2), label, ha='center', va='center')

    plt.show()

# Example events
events = [
    ("09:00", "10:30", "Meeting 1"),
    ("11:00", "12:30", "Meeting 2"),
    ("13:30", "14:30", "Lunch"),
    ("15:00", "16:30", "Meeting 3"),
    ("17:00", "18:00", "Coffee Break")
]

circular_day_planner(events)
