---
title: "Foundation of Computer Science"
---
<section>
  <h2>Request</h2>
  <div id="student-request" style="clear: both;">
      <form name="submit-to-google-sheet" id="submit-to-google-sheet" onsubmit="alert('Your request has been submitted. The page will automatically be updated after a few seconds.')">
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
        <iframe id="queuing-iframe" name="queuing-iframe" src="https://docs.google.com/spreadsheets/d/12O-1mD3zoCPbDc-oz1cZRwD7ou_lbGLKKZu-hN4vur4/gviz/tq?tqx=out:html&tq&gid=0" frameborder="0" width="100%" height="2000px" allowfullscreen></iframe>
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
        document.getElementById("submit-to-google-sheet").reset();
        ToggleStatus();
      })
      .catch(error => console.error('Error!', error.message));
  })

</script>