---
---
<script src="assets/js/sorttable.js"></script>

<details open>
<summary>
Why does this exist?
</summary>
Summary to be written.
	
In short, US DoD Defense Contractors who have the requirements to implement NIST SP 800-171 on their Covered Contractor Information Systems must use FIPS 140 Validated Cryptography when protecting the confidentiality of Controlled Unclassified Information (CUI). Many Applications break when such cryptography is enforced, and many vendors charge a surcharge or hide this cryptography under a premium license.
</details>

{% assign all = site.vendors | sort: "name" %}
{% assign vendors = "" | split: ',' %}
{% assign call_us = "" | split: ',' %}
{% for vendor in all %}
	{% if vendor.sso_pricing contains "Call" %}
		{% assign call_us = call_us | push: vendor %}
	{% else %}
		{% assign vendors = vendors | push: vendor %}
	{% endif %}
{% endfor %}

## Applications that break while utilizing FIPS
Vendors listed here have programs/products that break in significant manners when FIPS cryptography is enabled on a host machine. 

<table class="sortable">
<thead>
<tr><th>Vendor</th><th>Base Pricing</th><th>% Increase</th><th>Source</th><th>Date Updated</th></tr>
</thead>
<tbody>
{% for vendor in vendors %}
<tr>
<td markdown="span"><a href="{{ vendor.vendor_url }}">{{ vendor.name }}</a></td>
<td markdown="span">{{ vendor.base_pricing }}</td>
<td markdown="span">{{ vendor.percent_increase }}</td>
<td>
{% for source in vendor.pricing_source %}
{% if forloop.first == false %}
&amp;
{% endif %}
<a href="{{ source }}">&#128279;</a>
{% endfor %}
{{ vendor.pricing_note }}</td>
<td>{{ vendor.updated_at }}</td>
</tr>
{% endfor %}
</tbody>
</table>

## Vendors that charge a premium for FIPS ##
Some vendors simply do not list their pricing for FIPS because the pricing is negotiated with an account manager. These vendors get their own table as we assume they apply a significant premium for FIPS.

<table class="sortable">
<thead>
<tr><th>Vendor</th><th>Base Pricing</th><th>FIPS Pricing</th><th>% Increase</th><th>Source</th><th>Date Updated</th></tr>
</thead>
<tbody>
{% for vendor in call_us %}
<tr>
<td markdown="span"><a href="{{ vendor.vendor_url }}">{{ vendor.name }}</a></td>
<td markdown="span">{{ vendor.base_pricing }}</td>
<td markdown="span">{{ vendor.sso_pricing }}</td>
<td markdown="span">{{ vendor.percent_increase }}</td>
<td>
{% for source in vendor.pricing_source %}
{% if forloop.first == false %}
&amp;
{% endif %}
<a href="{{ source }}">&#128279;</a>
{% endfor %}
{{ vendor.pricing_note }}</td>
<td>{{ vendor.updated_at }}</td>
</tr>
{% endfor %}
</tbody>
</table>

## FAQs

<details>
<summary>
This doesn't scale linearly for number of seats!
</summary>
Correct. Since we don't know who's reading the page, it's easiest to just assume a team with no volume discount.
</details>

<details>
<summary>
How is base pricing determined?
</summary>
We disregard free tier pricing, as we can assume these aren't intended for long term business customer use. We also disregard "single person" pricing, under the assumption that we're looking on behalf of a team of 5, 10, or more people.
</details>

<details>
<summary>
What does "Quote" mean in the Source column?
</summary>
If a vendor doesn't list pricing but a user has submitted pricing based on a quote, it can be included here. If a vendor feels that their actual pricing is inaccurately reflected by this quote, feel free to let me know and I'll update the page.
</details>

<details>
<summary>
I'm a vendor and this data is wrong!
</summary>
Please feel free to submit a PR to this page, or reach out at sso @ myGitHubUsername dotcom. I only want this data to be accurate.
</details>

<details>
<summary>
I'm a vendor and this doesn't reflect the value-add of our Enterprise tier!
</summary>
That's the point. Decouple your security features from your value-added services. They should be priced separately.
</details>

<details>
<summary>
But it costs money to get FIPS Validation, so we can't offer it for free!
</summary>
  TBD
</details>

## Footnotes
{% for vendor in vendors %}
{{ vendor.footnotes }}
{% endfor %}
{% for vendor in call_us %}
{{ vendor.footnotes }}
{% endfor %}
