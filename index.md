---
title: "Foundation of Computer Science"
---

<!-- get current time -->
{% assign current_hour = site.time | date: "%k" | plus:0 %}
{% assign current_week_day = site.time | date: "%w" | plus:0 %}

{% if current_hour >= 13 and current_hour =< 15 and current_week_day > 0 and current_week_day < 3 %}
  <section>
    <h2>Request</h2>
    <div id="student-request" style="clear: both;">
        <form name="submit-to-google-sheet">
            <label style="display: inline-block; width: 150px;">Student name</label>
            <input name="student_name" placeholder="Your name" required/>
            <br />
            <label style="display: inline-block; width: 150px;">Room number</label>
            <input name="room_number" placeholder="8"/>
            <br />
            <label style="display: inline-block; width: 150px;">Inquiry</label>
            <input name="inquiry" placeholder="Mark assignment 1"/>
            <br />
            <input name="status" placeholder="" hidden/>
            <br />
            <button type="submit">Send</button>
        </form>
    </div>
  </section>

  <br />

  <!-- display Google Sheet data -->
  <section>
      <h2>Queuing list</h2>
      <div>
          <iframe id="queuing-iframe" name="queuing-iframe" src="https://docs.google.com/spreadsheets/d/12O-1mD3zoCPbDc-oz1cZRwD7ou_lbGLKKZu-hN4vur4/gviz/tq?tqx=out:html&tq&gid=0" frameborder="0" width="100%" height="500px" allowfullscreen></iframe>
      </div>
  </section>

  <!-- script to retrieve data from Google Sheet -->
  <script>
    const scriptURL = 'https://script.google.com/macros/s/AKfycbzKyYvMuAA1infTOVQ7EJcnhshD2SKac3xI8m5T3n5rtq8_il3nOg7nQQNoVvKG78OoAA/exec';
    const form = document.forms['submit-to-google-sheet'];

    form.addEventListener('submit', e => {
      e.preventDefault();
      fetch(scriptURL, { method: 'POST', body: new FormData(form)})
        .then(response => console.log('Success!', response))
        .then(response => {
          // refresh iframe
          queu_iframe = document.getElementById('queuing-iframe');
          queu_iframe.parentNode.replaceChild(queu_iframe.cloneNode(), queu_iframe);
        })
        .catch(error => console.error('Error!', error.message));
    })

  </script>
{% else %}
  <div>
    Workshop session has not been started yet. Please come back on Monday or Tuesday from 1:00 PM to 3:00 PM.
  </div>
{% endif %}