Using POSTGRESQL with ASP.NET Core
==================================


> **To get the project started, in Visual Studio 2017:**
> * Start a "New Project"
> * Select "Web"
> * Select "ASP.NET Core Web Application"
> * Select "Web Application (Model-View-Controller)"
> * Click Change Authentication
> * Change the Authentication to "Individual User Accounts"
> * Select "Store user accounts in-app"
> * Click "OK"
> * Click "OK' to create the project.

> **In order to take out the SQL Server dependencies, you need to do the following inside the AspDotNet Core project:**

> * Add the nuget package: 

    "Npgsql.EntityFrameworkCore.PostgreSQL"

> * In the Startup.cs file, remove the code that says:

	services.AddDbContext<ApplicationDbContext>(options =>
		options.UseSqlServer(Configuration.GetConnectionString("DefaultConnection")));

> * Replace it with code that says:

	services
		.AddEntityFrameworkNpgsql()
		.AddDbContext<ApplicationDbContext>(options =>
			options.UseNpgsql(Configuration.GetConnectionString("DefaultConnection"))
		);

> * Remove the connection string out of app settings.
> * Put your POSTGRES connection string into app secrets...
> * Right click on the project file in the Solution Explorer
> * Click "Manage User Secrets".
> * Add the following code into the User Secrets file:

	{
		"DefaultConnection": "Server=localhost;Database=MyDatabaseName;username=MyUserName;password=p@ssw0rd"
	}

> * Replace "MyDatabaseName" with the name of your database.
> * Also, replace "MyUserName", and "p@ssw0rd"

> **Add the Entity Framework changes to your database:**

> * In the directory with your project, run the following console command:

	dotnet ef migrations add InitialCreate

>   *Now your database is prepared to push up to the POSTGRES database..*
> * Now run the following console command:

	dotnet ef database update
	
>   *Now your database should be updated with the changes.*
