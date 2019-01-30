# Tiny C++ wrapper around littlevgl library

Only a label and a button, for the workshop.

Example:

```cpp
#include <mbed.h>
#include <gui.h>

GUI gui;     /* our GUI instance */
Label lbl;   /* label in the global scope, we will change text from the button callback */
int cnt = 0; /* click counter */

/* button callback */
static void callback(Button * b){
  cnt++;
  char msg[40];
  sprintf(msg, "Button clicked %d times!", cnt);
  lbl.text(msg);
}

int main() {

  gui.init();

  /* Create a label to log clicks */
  lbl = gui.label("Hello display!");
  lbl.size(gui.width(), 100); // full width
  lbl.position(0, 200);
  lbl.align_text(ALIGN_TEXT_CENTER);

  /* Create a button */
  Button btn = gui.button(callback, "Click me!");
  btn.size(300, 100);
  btn.position(0, 300);
  btn.align(ALIGN_CENTER);

  while(1) {
    gui.update();
  }
}
```
