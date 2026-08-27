# 054: sending an image, and what it costs

builds on: [053](./053-what-to-leave-out.md), [045](./045-roles-are-markers.md), [004](./004-tokens-are-money.md)
arc: the prompt is the program (10 of 11), ~2 min

053 had me pricing every line in that array. an image is another line, and i had no number for it.

```
the array from 045. content is a list of parts now

  {
    "role": "user",
    "content": [
      {"type": "text",  "text": "which dropdown is cut off?"},
      {"type": "image", "source": {"type": "base64",
                                   "media_type": "image/png",
                                   "data": "iVBORw0KGgoAAA..."}}
    ]                                       ^
  }                                         the whole file as text. a huge
                                            string, and nobody counts its
                                            characters

the screenshot is 900 x 1200. it gets cut into 28 pixel squares

  across    900 / 28 = 32.1  ->  33 squares (a part of one still counts)
  down     1200 / 28 = 42.9  ->  43 squares
  ----------------------------------------------------------------
  image part                33 x 43 =  1,419 tokens
  text part, roughly                       7 tokens
  this one message                     1,426 tokens

  the same screenshot at 600 x 800       638 tokens
```

no upload endpoint, no separate call. same post from 045, content just goes from a string to a list of parts.

the cost is the part i had wrong. i assumed a big base64 string meant a big bill, every other line in the array is priced by its characters. not this one. the image gets cut into a grid and you pay per square, so cost tracks area. a blank white screenshot costs the same as a crowded street photo the same size. nothing here looks at whats in the picture, it just measures it.

which gives you the easiest cut in the 053 table. resize first. that shot at 600 x 800 is 638 tokens and the dropdown is still perfectly visible. when did you last resize before posting to an api? i never had.

28 is one providers square, others use bigger tiles. send something enormous and it gets scaled down first, so theres a ceiling.

055 is the capstone, one real prompt built out of the whole arc.
