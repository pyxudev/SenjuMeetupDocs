# Example
## Specification Document
### Goal
- User should get an estimate in screen.

### Must have
- Title
- Basice information (date, number, name...)
- User information
- Interface to input information
- Displaying information
- Price data for each item
- Total price

### Better to have
- Delivery suggestions
- Download PDF file as output

### UI items
| Item name                           | Method            | Format           |
| --                                  | --                | --               |
| Estimate name                       | Fixed-String      | Estimate         |
| Estimate number                     | Auto-Id           | Id               |
| User(Company) name                  | input-String      | Text             |
| Date                                | Date              | yyyy/MM/dd       |
| Product name                        | <option>-String   | Pulldown         |
| Number for each product             | input-Int         | Number           |
| Reciver information                 | textarea-String   | Text with return |
| Provider information                | textarea-String   | Text with return |
| Reciver Post code                   | Postcode-Int      | 000-0000         |
| Reciver address                     | Textarea-String   | Textarea         |
| Delivery solution(nice to have)   | option-String     | Pulldown         |
| Estimate button(could be auto)      | button            | Onclick          |
| PDF download button(nice to have) | button            | Onclick          |
