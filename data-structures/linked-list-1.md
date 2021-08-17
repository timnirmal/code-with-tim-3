# Linked List



### Traversing a Linked List

Traversing a linked list means accessing the nodes of the list in order

{% tabs %}
{% tab title="Traversing" %}
```text
Step 1: [INITIALIZE] SET PTR = START
Step 2: Repeat Steps 3 and 4 while PTR != NULL
Step 3:         Apply Process to PTR DATA
Step 4:         SET PTR = PTR NEXT
        [END OF LOOP]
Step 5: EXIT
```
{% endtab %}

{% tab title="Number of Nodes" %}
```
Step 1: [INITIALIZE] SET COUNT = 0
Step 2: [INITIALIZE] SET PTR = START
Step 3: Repeat Steps 4 and 5 while PTR != NULL
Step 4:     SET COUNT = COUNT + 1
Step 5:     SET PTR = PTR -> NEXT
        [END OF LOOP]
Step 6: Write COUNT
Step 7: EXIT
```
{% endtab %}
{% endtabs %}

### Search a Linked Listed

```text
Step 1: [INITIALIZE] SET PTR = START
Step 2: Repeat Step 3 while PTR != NULL
Step 3:     IF VAL = PTR DATA
                SET POS = PTR
                Go To Step 5
             ELSE
                SET PTR = PTR NEXT
             [END OF IF]
         [END OF LOOP]
Step 4: SET POS = NULL
Step 5: EXIT
```

### Inserting a New Node in a Linked List

{% tabs %}
{% tab title="Beginning " %}
```text
Step 1: IF AVAIL = NULL
                Write OVERFLOW
                Go to Step 7
                [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET NEW_NODE -> NEXT = START
Step 6: SET START = NEW_NODE
Step 7: EXIT
```
{% endtab %}

{% tab title="End" %}
```
Step 1: IF AVAIL = NULL
                Write OVERFLOW
                Go to Step 10
        [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET NEW_NODE -> NEXT = NULL
Step 6: SET PTR = START
Step 7: Repeat Step 8 while PTR -> NEXT != NULL
Step 8:     SET PTR Step
        [END OF LOOP]
Step 9: SET PTR -> NEXT = NEW_NODE
Step 10: EXIT
```
{% endtab %}

{% tab title="Before" %}
```
Step 1: IF AVAIL = NULL
            Write OVERFLOW
            Go to Step 12
        [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET PTR = START
Step 6: SET PREPTR = PTR
Step 7: Repeat Steps 8 and 9 while PTR -> DATA != NUM
Step 8:     SET PREPTR = PTR
Step 9:     SET PTR = PTR NEXT
        [END OF LOOP]
Step 1 : PREPTR -> NEXT = NEW_NODE
Step 11: SET NEW_NODE -> NEXT = PTR
Step 12: EXIT
```
{% endtab %}

{% tab title="After" %}
```
Step 1: IF AVAIL = NULL
            Write OVERFLOW
            Go to Step 12
        [END OF IF]
Step 2: SET NEW_NODE = AVAIL
Step 3: SET AVAIL = AVAIL -> NEXT
Step 4: SET NEW_NODE -> DATA = VAL
Step 5: SET PTR = START
Step 6: SET PREPTR = PTR
Step 7: Repeat Steps 8 and 9 while PREPTR -> DATA
            != NUM
Step 8:             SET PREPTR = PTR
Step 9:             SET PTR = PTR NEXT
            [END OF LOOP]
Step 1 : PREPTR -> NEXT = NEW_NODE
Step 11: SET NEW_NODE -> NEXT = PTR
Step 12: EXIT
```
{% endtab %}
{% endtabs %}







