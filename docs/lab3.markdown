---
layout: default
title: "Lab 3: Mad Libs Project"
permalink: /lab-3/
---

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

  <div class="post-content e-content" itemprop="articleBody">
    <form method="get" id="form">
      <div class="form-group">
        <label for="noun">Person (Noun)</label>
        <input type="text" name="person" id="person" class="form-input" />
      </div>
      <div class="form-group">
        <label for="verb">Company (Noun)</label>
        <input type="text" name="company" id="company" class="form-input" />
        </div>
        <div class="form-group">
      <label for="adjective">Size (Adjective)</label>
      <input type="text" name="size" id="size" class="form-input" />
        </div>
        <div class="form-group">
      <label for="adjective">City (Noun)</label>
      <input type="text" name="city" id="city" class="form-input" />
        </div>
        <div class="form-group">
      <label for="adjective">Number (Noun)</label>
      <input type="number" name="number" id="number" class="form-input" />
        </div>
        <div class="form-group">
      <label for="adjective">Product (Noun)</label>
      <input type="text" name="product" id="product" class="form-input" />
        </div>
        <div class="form-group">
      <label for="adjective">Plural Noun</label>
      <input type="text" name="plural" id="plural" class="form-input" />
        </div>
        <div class="form-group">
      <label for="adjective">Verb</label>
      <input type="text" name="verb" id="verb" class="form-input" />
        </div>
        <div class="form-group">
      <label for="adjective">Adverb</label>
      <input type="text" name="adverb" id="adverb" class="form-input" />
        </div>
        <div class="form-group">
      <label for="adjective">"-ing" Verb (Gerund)</label>
      <input type="text" name="gerund" id="gerund" class="form-input" />
        </div>
      <input type="submit" value="Submit" />
    </form>
    <!-- render the form input to the page and convert them to query params -->
    <div id="story"></div>
    <script>
        var form = document.getElementById("form");
        var story = document.getElementById("story");
        story.style.display = "none";
        form.addEventListener("submit", function(event) {
            form.style.display = "none";
            var person = document.getElementById("person").value;
            var company = document.getElementById("company").value;
            var size = document.getElementById("size").value;
            var city = document.getElementById("city").value;
            var number = document.getElementById("number").value;
            var product = document.getElementById("product").value;
            var plural = document.getElementById("plural").value;
            var verb = document.getElementById("verb").value;
            var adverb = document.getElementById("adverb").value;
            var gerund = document.getElementById("gerund").value;
            var template = `Hello! My name is ${person}, and I am the founder and CEO of ${company}. We are a(n) ${size} company that is publicly traded on the ${city} Stock Exchange. We are currently valued at ${number} US Dollars. We sell a ${product} that helps ${plural} ${verb} ${adverb}. If you like ${gerund}, come work for us!`;
            story.innerHTML = template;
            story.style.display = "block";
            story.innerHTML += `<p><a href="${window.location.pathname}">Try new words!</a></p>`;
        });
        var urlParams = new URLSearchParams(window.location.search);
        if (urlParams.get("person") && urlParams.get("company") && urlParams.get("size") && urlParams.get("city") && urlParams.get("number") && urlParams.get("product") && urlParams.get("plural") && urlParams.get("verb") && urlParams.get("adverb") && urlParams.get("gerund")) {
            form.style.display = "none";
            var person = urlParams.get("person");
            var company = urlParams.get("company");
            var size = urlParams.get("size");
            var city = urlParams.get("city");
            var number = urlParams.get("number");
            var product = urlParams.get("product");
            var plural = urlParams.get("plural");
            var verb = urlParams.get("verb");
            var adverb = urlParams.get("adverb");
            var gerund = urlParams.get("gerund");
            var template = `Hello! My name is ${person}, and I am the founder and CEO of ${company}. We are a(n) ${size} company that is publicly traded on the ${city} Stock Exchange. We are currently valued at ${number} US Dollars. We sell a ${product} that helps ${plural} ${verb} ${adverb}. If you like ${gerund}, come work for us!`;
            story.innerHTML = template; 
            story.style.display = "block";
            story.innerHTML += `<p><a href="${window.location.pathname}">Try new words!</a></p>`;
        }
    </script>
    <style>
        .form-input {
            width: 100%;
        }
        .form-group {
            margin-bottom: 1rem;
        }
    </style>
  </div>
</article>