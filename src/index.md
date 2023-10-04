---
layout: default
---

{% assign events_by_date = site.data.events | sort: "start_date" | reverse %}
{% assign latest = events_by_date | first %}

Euruko is a Ruby conference organised annually, each year in a different European city chosen by the participants.

Every year the Ruby community from Europe and beyond come to Euruko to meet and share their love of Ruby. This is is the longest running and biggest Ruby conference anywhere in Europe and one of the biggest in the world.

It's up to the participants to pick the next city where the conference will be held. Attendees will pitch their own cities to be the hosts of the next year's conference which are then voted on by the audience. This also means that the conference organisers will change every year.

**Latest event:** [Euruko {{ latest.start_date | date: '%Y' }}]({{ latest.url }})

---

<table>
  <thead>
    <tr>
      <th>Year</th>
      <th>Location</th>
      <th>Dates</th>
    </tr>
  </thead>
  <tbody>
    {% for event in events_by_date %}
      <tr>
        <td>
          <a href="{{ event.url }}">{{ event.start_date | date: '%Y' }}</a>
        </td>
        <td>
          {{ event.location }}
          {% if event.notes %}
            ({{ event.notes }})
          {% endif %}
        </td>
        <td>
          {% # If the start day is the first of January, assume that the date hasn't been set yet -%}
          {% assign start_month_day = event.start_date | date: '%m-%d' %}
          {% if start_month_day == '01-01' %}
            TBD
          {% elsif event.start_date == event.end_date %}
            {{ event.start_date | date: '%-d %B %Y' }}
          {% else %}
            {% assign start_month = event.start_date | date: '%m' %}
            {% assign end_month = event.end_date | date: '%m' %}
            {% if start_month == end_month %}
              {{ event.start_date | date: '%-d' }}–{{ event.end_date | date: '%-d %B %Y' }}
            {% else %}
              {{ event.start_date | date: '%-d %b' }} – {{ event.end_date | date: '%-d %B %Y' }}
            {% endif %}
          {% endif %}
        </td>
      </tr>
    {% endfor %}
  </tbody>
</table>
