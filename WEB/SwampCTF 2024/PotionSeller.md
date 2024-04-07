This challenge involves a web application built with Express.js that simulates a potion shop. The objective is to retrieve the FLAG by fulfilling a specific condition.

![image](https://github.com/nhattanhh/CTF/assets/130430279/da0b76ce-a762-45ec-bb7e-eba2478600e0)

![image](https://github.com/nhattanhh/CTF/assets/130430279/e4a231ff-556f-4ca4-826d-a91a406ce9ef)

The provided source code reveals that to obtain the FLAG, we need to set the req.session.user.swampShade value to true. This can be achieved by purchasing the "Swampshade Serum" potion, which has an ID of 4.

![image](https://github.com/nhattanhh/CTF/assets/130430279/b400eab0-5215-4871-bda5-dd47e9cd13e0)

![image](https://github.com/nhattanhh/CTF/assets/130430279/a9b6b66f-8d3a-45a4-8aac-5b56b28d9ccb)

But you can't buy that, because you haven't enough gold, so that you have to borrow:

![image](https://github.com/nhattanhh/CTF/assets/130430279/e82b41a6-167e-4e7f-a170-c3755f0f307d)

By this borrow's function

![image](https://github.com/nhattanhh/CTF/assets/130430279/5c9f1018-ee67-4c9b-a7e5-cc44cc4e0cd6)

Try to borrow 1000 with 'amount' parameters:

![image](https://github.com/nhattanhh/CTF/assets/130430279/b93d83fb-b413-4858-9564-4920b030d105)

So try to buy again the potion and we got this:

![image](https://github.com/nhattanhh/CTF/assets/130430279/87bd599e-88f2-4ffc-a395-de4070a8f790)

Alright! Now trying to check out for flag:
But we still missing sthg...
Argg! we still have a debt ...

![image](https://github.com/nhattanhh/CTF/assets/130430279/9059cf14-687b-4121-bed6-777bc335119a)

![image](https://github.com/nhattanhh/CTF/assets/130430279/ce237725-e312-4dc4-85b2-30a26e39ef35)

Just repay all of that with /repay?amount=?

![image](https://github.com/nhattanhh/CTF/assets/130430279/c14ad82b-fe33-4126-9f6c-9a89f51c4b8a)

/checkout again~.~

![image](https://github.com/nhattanhh/CTF/assets/130430279/49ea6885-e7fa-4837-ac13-967194b8ea1b)

Alright!
