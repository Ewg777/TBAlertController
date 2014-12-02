TBAlertController
=================

UIAlertController, UIAlertView, and UIActionSheet unified for develoeprs who want to support iOS 7 and 8.

TBAlertController tries to be as much of a drop-in replacement for all three classes as possible. TBAlertController objects will respond to `show`, `showInView:`, and implements it's own `showFromViewController:animated:completion:` (as well as a simpler `showFromViewController:`).

The only major difference for iOS 7 is that TBAlertController does away with delegates in favor of block and target-selector style actions. Delegate support will not be added, since this project is directed at developers who want to minimize code involving action sheets and alert views on iOS 7 and 8. It is possible to use the same code for both platforms; TBAlertController takes care of the rest for you.

Examples:

            TBAlertController *alert = [[TBAlertController alloc] initWithStyle:TBAlertControllerStyleActionSheet];
            alert.title   = @"Alert";
            alert.message = @"This is a message!";
            [alert addOtherButtonWithTitle:@"OK" onTapped:^{ [self pressedOK]; }];
            [alert addOtherButtonWithTitle:@"Delete" target:self action:@selector(selfDestruct)];
            [alert setCancelButtonWithTitle:@"Cancel"];
            alert.destructiveButtonIndex = 1;

This will create an action sheet with the title `Alert` and a message, as well as three buttons: `OK` with a block style action, `Delete` with a target-selector style action (as well as being the "destructive" button), and a `Cancel` button which only dismisses the alert. The cancel button will always appear last in the list of buttons if set using one of the `setCancelButton...` methods.

Actions can be added to any button, either block or target-selector style. Destructive buttons can only be added when using `TBAlertControllerStyleActionSheet` on iOS 7. Buttons can also be added with just a title.

The target-selector style actions also support passing a single parameter, like `performSelector:withObject:`.

            TBAlertController *alert = [[TBAlertController alloc] initWithTitle:@"Title"
                                                                        message:@"Hello world"
                                                                          style:TBAlertControllerStyleActionSheet];
            [alert addOtherButtonWithTitle:@"Dismiss"];
            [alert addOtherButtonWithTitle:@"Say hi" target:self action:@selector(say:) withObject:@"hi"];

TODO
- Add support for alert views with text boxes.