# The Everything Remote

A simple universal remote designed for ESPHome - simple to assemble for beginners and experienced tinkerers alike! 

<iframe width="560" height="315" src="https://www.youtube.com/embed/Pe_ozZkrRAw?si=tF58U9hxBXpLBO2W" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

---

## 📦 Features

- 24 configurable buttons (single press + long press)
- Works over Wi-Fi using ESPHome
- Sends `button_pressed` events to Home Assistant
- Deep sleep support for ultra-low power usage
- Supports `select`, `back`, `play/pause`, volume, brightness, navigation, and more
- Simple GPIO-based design (can be adapted to your own button layout)

---

## 🛠 Hardware Requirements

This project assumes you're using the [custom PCB](https://www.thestockpot.net/videos/theeverythingremote) and button matrix from the original build. However, you can adapt the software to any ESP32 board and button configuration.

**Minimum:**

- ESP32 (e.g., ESP32 DevKit v1)
- 24 momentary push buttons
- GPIO pins (see pinout below)
- Optional: touch input pin for waking from deep sleep

---

## 🧠 How It Works

Each button triggers an event via ESPHome’s `homeassistant.event` component. These events can then be used in Home Assistant to control anything — lights, media players, automations, etc.

Example:

```yaml
- platform: gpio
  pin: GPIO22
  id: select_button
  on_click:
    then:
      - homeassistant.event:
          event: esphome.button_pressed
          data:
            button: select
            type: single
