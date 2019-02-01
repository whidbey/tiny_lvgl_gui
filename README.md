# Tiny C++ wrapper around littlevgl library

Only a label and a button, for the workshop.

Example:

```cpp
#include <mbed.h>
#include <gui.h>

GUI gui;     /* our GUI instance */
Label lbl;   /* label in the global scope, we will change text from the button callback */

/* button callback, default lvgl type */
static lv_res_t callback(lv_obj_t * btn){
  Button button(btn); // can be converted to C++ class
  uint id = button.id();
  id++;
  button.id(id);
  char msg[40];
  sprintf(msg, "Button clicked %d times!", id);
  lbl.text(msg);
  return LV_RES_OK;
}

int main() {

  gui.init();

  // Create a label to log clicks
  lbl = Label("Hello display!");
  lbl.size(gui.width(), 100); // full width
  lbl.position(0, 200);
  lbl.align_text(ALIGN_TEXT_CENTER);

  // Create a button
  Button btn(callback, "Click me!");
  btn.id(0); // we will use id of a button as a counter.
  btn.size(300, 100);
  btn.position(0, 300);
  btn.align(ALIGN_CENTER);

  while(1) {
    gui.update();
  }
}
```
