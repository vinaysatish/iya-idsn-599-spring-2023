---
layout: default
title: "Lab 4: HR Directory"
permalink: /lab-4/
---

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Company HR Directory from a CSV File</title>
  <script src="https://d3js.org/d3.v6.min.js"></script>
</head>

<article
  class="post h-entry"
  itemscope
  itemtype="http://schema.org/BlogPosting"
>
  <header class="post-header">
    <h1 class="post-title p-name" itemprop="name headline">
      {{ page.title | escape }}
    </h1>
  </header>
  <div>
    {% for row in site.data.usc-users %}
        {% assign loopindex = forloop.index | modulo: 4 %}
        {% if loopindex == 1 %}
            <div class="row">
        {% endif %}
                <div class="column">
                    <div class="post-content e-content card" id="card-{{ forloop.index }}">
                        <img src="{{ row['picture.medium'] }}">
                        <p class="title">{{ row['name.first'] }} {{ row['name.last'] }}</p>
                        <p>{{ row['location.city'] }}, {{ row['location.state'] }}, {{ row['location.country'] }}, {{ row['location.postcode'] }}</p>
                        <p><a href="mailto:{{ row['email'] }}" title="{{ row['email'] }}">Email</a></p>
                        <p><a href="tel:{{ row['phone'] }}" title="{{ row['phone'] }}">Phone</a></p>
                    </div>
                </div>
        {% if loopindex == 0 %}
            </div>
        {% endif %}
    {% endfor %}
    <style>
        * {
            box-sizing: border-box;
        }
        p {
            margin: 5px 0;
        }
        .title {
            font-weight: bold;
            font-size: 18px;
        }
        .column {
            float: left;
            width: 25%;
            padding: 0 5px;
            display: flex;
        }
        .card {
            background-color: #f1f1f1;
            padding: 20px;
            margin-top: 20px;
            text-align: center;
            border-radius: 10px;
            width: 100%;
        }
        .row {
            margin: 0 -5px;
            display: flex;
            flex-wrap: wrap;
        }
        @media screen and (max-width: 600px) {
            .column {
                width: 100%;
                display: block;
                margin-bottom: 20px;
            }
        }
    </style>
  </div>