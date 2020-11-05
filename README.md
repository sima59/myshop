# myshop
Actually the first time when I added these code to the detail it worked fine then I deleted some items from my site in a admin page then when I reran it again it didn’t work. I don’t know if there are some IDs of deleted items somewhere in the cart and it looks for them and because couldn’t find them generate error or it has another reason. 

Cart\ Template\Detail.html 
When I added this code ,got the following error:
    <form action="{% url "cart:cart_add" product.id %}" method="post">
                {{ item.update_quantity_form.quantity }}
                {{ item.update_quantity_form.override }}
                <input type="submit" value="Update">
                {% csrf_token %}
              </form>
            </td>
            <td>
              <form action="{% url "cart:cart_remove" product.id %}" method="post">
                <input type="submit" value="Remove">
                {% csrf_token %}
              </form>

 


But when I remove it from Cart\ Template\Detail.html . It works fine. But I need remove options in my cart. 

{% extends "shop/base.html" %}
{% load static %}

{% block title %}
  Your shopping cart
{% endblock %}

{% block content %}
  <h1>Your shopping cart</h1>
  <table class="cart">
    <thead>
      <tr>
        <th>Image</th>
        <th>Product</th>
        <th>Quantity</th>
        <th>Remove</th>
        <th>Unit price</th>
        <th>Price</th>
      </tr>
    </thead>
    <tbody>
      {% for item in cart %}
        {% with product=item.product %}
          <tr>
            <td>
              <a href="{{ product.get_absolute_url }}">
                <img src="{% if product.image %}{{ product.image.url }}
                {% else %}{% static "img/no_image.png" %}{% endif %}">
              </a>
            </td>
           <td>{{ product.name }}</td>
           <td>{{ item.quantity }}</td>
           <td>
            {{ item.quantity }}
          </td>
             <td class="num">${{ item.price }}</td>
            <td class="num">${{ item.total_price }}</td>
          </tr>
        {% endwith %}
      {% endfor %}
      <tr class="total">
        <td>Total</td>
        <td colspan="4"></td>
        <td class="num">${{ cart.get_total_price }}</td>
      </tr>
    </tbody>
  </table>
  <p class="text-right">
    <a href="{% url "shop:product_list" %}" class="button
    light">Continue shopping</a>
    <a href="{% url "orders:order_create" %}" class="button">Checkout</a>
  </p>
{% endblock %}


I also got following message when place order. I can see the order added to the http://127.0.0.1:8000/admin/orders/order/ page but it doesn’t give me the confirmation. I don’t knoe what is wrong with product argument. Both errors related to it. I searched it but none of the recommended solution could fix my issue.


 



