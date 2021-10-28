# TableView 

### .reloadData()

**EN:**

.reloadData() is necessary for refreshing a tableView. If we are setting up an empty array of objects or tableView will not show up data even if we pass values to it. 
At the beginning our view is empty so tableView is not renedring cells. Thinks that count is equal 0. Acctually is equal to 0 because fetching takes some time to complete. 

**PL:**

.reloadData() jest niezbędny do odświeżenia naszego tableView. Jeśli tworzymy pusty zbiór/listę (jak chcesz to nazwać) i przypisujemy do niego pobrane dane ten podczas ładowania widoku jest pusty. 
W związku z tym tableView nie renderuje żadnej komórki gdyż jej po prostu nie ma. Jeśli po załadowaniu danych nie odświeżymy tableView ten ciągle będzie myślał, że nic nie zostało przekazane.

```swift


class NewMessageController: UITableViewController {
    
    private var users = [User]() // now our array count == 0

    override func viewDidLoad() {
        super.viewDidLoad()
        fetchUsers()
    }

    func fetchUsers() {
        Service.fetchUsers { users in
            self.users = users // if we fetch users count changes from 0 to number of users (from database)
            print("DEBUG: Users in new message are: \(users)")
            self.tableView.reloadData() // refresh tableView
        }
    }
}

extension NewMessageController {
    override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return users.count // while view is loading count is equal to 0, if we do not reloadData() it's still going to be 0 and our tableView do not display any cell
    }
    
    override func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell = tableView.dequeueReusableCell(withIdentifier: reusableIdentifier, for: indexPath) as! UserCell
        return cell
    }
}


```
