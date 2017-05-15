SDF TextField Validation
==================

Add simple validation to your text fields for the following types:

- **none**: default
- **email**: Needs an @ and a TLD.
- **email optional**: as above but can also be empty
- **password**: requires at least 1 character, masked text.
- **required**: requires at least 1 character.

# Usage

1. Add the following line to your header

	```
	#import "NSTextField+Validation.h"
	```

2. Set a **textFieldValidationType** property to the NSTextField from the **TextFieldValidationType** enum.

	```
	// Where self.textField is an NSTextField property on the class
	self.textField.textFieldValidationType = TextFieldValidationTypeEmail;
	```
	
3. Set a placeholder string if required (not required if you have the text field linked up in the nib and the placeholder set there)

	```
	self.textField.placeholderString = @"Email";
	```

4. Add **NSTextFieldDelegate** to the .h file.
5. Add the following to the .m file.
	
	```
	#pragma mark - Notification
	
	- (void)controlTextDidChange:(NSNotification *)notification
	{
		NSTextField *textField = [notification object];
		BOOL valid = [textField validate];
		if (!valid) {
		  // Do something on invalid entry if you want
		}
	}
	```

It is at this point the fields will be highlighted based on the validation type you set.

# Methods

- **valid**: This will check the current string of the text field against the validation type and return the result.
- **reset**: Reset the text field removing all validation background colouring.

# Customisation

Setting the colours is easy, just modify your colours as required. All take an NSColor as type.

- [NSTextField setBackgroundColour:colour];
- [NSTextField setValidBackgroundColour:colour];
- [NSTextField setInvalidBackgroundColour:colour];
- [NSTextField setPlaceholderFontColour:colour];
- [NSTextField setPlaceholderValidateFontColour:colour];

**Defaults**

Each field has it's own default as specified below:

- kValidationTextFieldBackgroundColour = [NSColor whiteColor];
- kValidationTextFieldValidBackgroundColour = [NSColor greenColor];
- kValidationTextFieldInvalidBackgroundColour = [NSColor redColor];
- kValidationTextFieldPlaceholderValidateFontColour = [NSColor whiteColor];
- kValidationTextFieldPlaceholderFontColour = [NSColor grayColor];
