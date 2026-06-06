# Calulater_by_Python
By this code you can calculate the four basic mathematical operations via python.


import ipywidgets as widgets
from IPython.display import display

# Display
display_box = widgets.Text(
    value='',
    placeholder='Enter calculation',
    description='Calc:',
    layout=widgets.Layout(width='400px')
)

# Button layout
buttons = [
    ['7', '8', '9', '/'],
    ['4', '5', '6', '*'],
    ['1', '2', '3', '-'],
    ['0', '.', 'C', '+']
]

button_widgets = []

for row in buttons:
    row_buttons = []
    for text in row:
        row_buttons.append(
            widgets.Button(
                description=text,
                layout=widgets.Layout(width='60px', height='50px')
            )
        )
    button_widgets.append(widgets.HBox(row_buttons))

equal_button = widgets.Button(
    description='=',
    layout=widgets.Layout(width='245px', height='50px')
)

# Event handler
def on_click(b):
    value = b.description

    if value == 'C':
        display_box.value = ''
    else:
        display_box.value += value

def on_equals(b):
    try:
        display_box.value = str(eval(display_box.value))
    except:
        display_box.value = 'Error'

# Connect buttons
for row in button_widgets:
    for btn in row.children:
        btn.on_click(on_click)

equal_button.on_click(on_equals)

# Show calculator
display(display_box)

for row in button_widgets:
    display(row)

display(equal_button)
