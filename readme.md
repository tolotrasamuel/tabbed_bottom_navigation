# Tabbed Bottom Navigation Bar
## Motivation:

https://stackoverflow.com/questions/76800833/how-navigate-directly-to-sibling-widgets-in-flutter-without-going-back

The goal is :

- a) Prevent tab change when user is editing something, have a callback confirming user to discard unsaved changes
- b) Deep Linking on tabs, and sub pages after each tabs
- c) Returning to the root page , not on tab changes, but on Navigation Pop only (all 3 tabs popped)
- d) Tab change smooth animation
- e) First tab push smooth animation

There are 3 options: 
1) Use Flutter TabView
2) Using a page for each Tab with Navigation.of(context).pushReplacement();
3) Using a page for each Tab with custom Tab wrapper wrapper


Issues: 

1) Use Flutter TabView
You can get a callback from the Children tabs to confirm the tab change. Use GlobalKey will be so complicated and non versatile
Goal compromised: a)

2) Using a page for each Tab with Navigation.of(context).pushReplacement();
`pushReplacement` would pop the first pushed tab page, and ending the Future awaited at the root on tab change
Goal compromised: c)

3)   Using a page for each Tab with custom Tab wrapper wrapper
A proxy widget is used between the root and the tabs. On tab tapped, Pop is used with the tapped tab as parameter to the awaiting proxy widget.
The proxy widget the checks if this is a widget to push, if so, it pushes it back. If not, it pops itself back to the root with whatever popped value from the last popped tab.
Goal compromised: d) e)
- 
```
Root -> Tab 1
     -> Tab 2
     -> Tab 3
```
The issue is that with 

With noraml Flutter Tabs, You can't have 
