


// Klasa Book

    
    public class Book
    {
    public string Title { get; set; }
    public string Author { get; set; }

    public Book(string title, string author)
    {
        Title = title;
        Author = author;
    }
    }

// Klasa User

    public class User
    {
    public string Name { get; set; }
    public int ID { get; set; }
    public int MaxLoanDays { get; set; }
    public Book RentedBook { get; set; }

    public User(string name, int id)
    {
        Name = name;
        ID = id;
        MaxLoanDays = 30;
    }

    public virtual void DisplayInfo()
    {
        Console.WriteLine($"[User] {Name} (ID {ID}) | Max Loan Days: {MaxLoanDays} days");

        if (RentedBook != null)
            Console.WriteLine($"  Rented: \"{RentedBook.Title}\" by {RentedBook.Author}");
        else
            Console.WriteLine("  No book currently rented.");
    }
    }

// Dziedziczenie | Override

    class PremiumUser : User
    {
    public string MembershipType { get; set; }

    public PremiumUser(string name, int id, string membershipType) : base(name, id)
    {
        MembershipType = membershipType;
        MaxLoanDays = 45;
    }

    public override void DisplayInfo()
    {
        Console.WriteLine($"[Premium User] {Name} (ID {ID}) | Membership: {MembershipType} | Max Loan Days: {MaxLoanDays} days");

        if (RentedBook != null)
            Console.WriteLine($"  Rented: \"{RentedBook.Title}\" by {RentedBook.Author}");
        else
            Console.WriteLine("  No book currently rented.");
    }
    }

    class Program
    {
    static void Main(string[] args)
    {
        Book book1 = new Book("Pride and Prejudice", "Jane Austen");
        Book book2 = new Book("The Great Gatsby", "F. Scott Fitzgerald");
        Book book3 = new Book("Dune", "Frank Herbert");
        Book book4 = new Book("Metamorphosis", "Franz Kafka");

        User user1 = new User("Don Mayer", 992884);
        user1.RentedBook = book1;

        PremiumUser premiumUser1 = new PremiumUser("Laura Gilbert", 729331, "Premium");
        premiumUser1.RentedBook = book2;

        PremiumUser premiumUser2 = new PremiumUser("Sarah Smith", 221468, "Premium");
        premiumUser2.RentedBook = book3;

        User user2 = new User("Tom Glanderson", 112932);
        user2.RentedBook = book4;

        User user3 = new User("Christine Peterson", 900826);

        List<User> allUsers = new List<User>() { user1, premiumUser1, premiumUser2, user2, user3 };

        
        DisplayRentedBooksStatus(allUsers);
      }

    
      static void DisplayRentedBooksStatus(List<User> allUsers)
      {
        Console.WriteLine("=== All Library Members ===\n");

        foreach (User user in allUsers)
        {
            user.DisplayInfo();
            Console.WriteLine();
        }

        
        DisplayRentalStats(allUsers);
    }

    static void DisplayRentalStats(List<User> users)
    {
        int totalMembers = users.Count;
        int rentedCount = users.Count(u => u.RentedBook != null);
        int notRentedCount = totalMembers - rentedCount;

        Console.WriteLine("=== Rental Statistics ===\n");
        Console.WriteLine($"  Total Members   : {totalMembers}");
        Console.WriteLine($"  Books Rented    : {rentedCount}");
        Console.WriteLine($"  No Book Rented  : {notRentedCount}");
        Console.WriteLine();
    }
    }
