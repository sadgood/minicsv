# Introduction #

Example of writing tab-separated values into file.
```
#include "minicsv.h"

struct Product
{
    Product() : name(""), qty(0), price(0.0f) {}
    Product(std::string name_, int qty_, float price_) 
        : name(name_), qty(qty_), price(price_) {}
    std::string name;
    int qty;
    float price;
};

int main()
{
    csv::ofstream os("products.txt", std::ios_base::out);
    os.set_delimiter('\t');
    if(os.is_open())
    {
        Product product("Shampoo", 200, 15.0f);
        os << product.name << product.qty << product.price << NEWLINE;
        Product product2("Soap", 300, 6.0f);
        os << product2.name << product2.qty << product2.price << NEWLINE;
    }
    os.close();
    return 0;
}
```

Example of reading tab-separated values from file.

```
#include "minicsv.h"
#include <iostream>

int main()
{
    csv::ifstream is("products.txt", std::ios_base::in);
    is.set_delimiter('\t');
    if(is.is_open())
    {
        Product temp("Shampoo", 200, 15.0f);
        while(!is.eof())
        {
            is >> temp.name >> temp.qty >> temp.price;
            // display the read items
            std::cout << temp.name << "," << temp.qty << "," << temp.price << std::endl;
        }
    }
    return 0;
}

```