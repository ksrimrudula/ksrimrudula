 import cv2
import numpy as np
import random

class Cat:
    def __init__(self):
        self.position = [0, 0]  # Cat's position in the room

    def move(self):
        self.position[0] += random.randint(-1, 1)
        self.position[1] += random.randint(-1, 1)

class Rat:
    def __init__(self):
        self.position = [9, 9]  # Rat's initial position in the room

    def move(self):
        self.position[0] += random.randint(-1, 1)
        self.position[1] += random.randint(-1, 1)

def draw_objects(frame, cat_pos, rat_pos):
    # Draw cat and rat on the frame
    cv2.circle(frame, tuple(cat_pos), 20, (255, 0, 0), -1)  # Blue circle for cat
    cv2.circle(frame, tuple(rat_pos), 20, (0, 0, 255), -1)  # Red circle for rat

def main():
    # Initialize cat and rat
    cat = Cat()
    rat = Rat()

    # Open the camera
    cap = cv2.VideoCapture(0)

    while True:
        # Capture frame from camera
        ret, frame = cap.read()
        if not ret:
            print("Failed to capture frame")
            break

        # Move cat and rat
        cat.move()
        rat.move()

        # Draw objects on the frame
        draw_objects(frame, cat.position, rat.position)

        # Display the frame
        cv2.imshow('AR Cat and Rat', frame)

        # Check for quit command
        if cv2.waitKey(1) & 0xFF == ord('q'):
            break

    # Release the camera and close OpenCV windows
    cap.release()
    cv2.destroyAllWindows()

if __name__ == "__main__":
    main()
