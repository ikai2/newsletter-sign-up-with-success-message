<script>
  let submitted = false;
  let email = '';
  let emailIsValid = true;
  function validateEmail(email) {
    const emailRegex = /^[\w-]+(?:\.[\w-]+)*@(?:[\w-]+\.)+[a-zA-Z]{2,7}$/;
    return emailRegex.test(email);
  }

  function handleSubmit(e) {
    const formData = new FormData(e.target);
    email = formData.get('email');
    emailIsValid = validateEmail(email);
    if (emailIsValid) {
      submitted = true;
    }
  }
  </script>

{#if !submitted}
    <div class="newsletter">
        <div class="newsletter-form">
            <div class="newsletter-info">
                <h1>Stay updated!</h1>
                <p>Join 60,000+ product managers receiving monthly updates on:</p>
                <ul>
                    <li><svg xmlns="http://www.w3.org/2000/svg" width="21" height="21" viewBox="0 0 21 21" fill="none">
                        <circle cx="10.5" cy="10.5" r="10.5" fill="#FF6155"/>
                        <path d="M6 11.3812L8.73464 14L15 8" stroke="white" stroke-width="2"/>
                        </svg>
                        <span>Product discovery and building what matters</span>
                    </li>
                    <li><svg xmlns="http://www.w3.org/2000/svg" width="21" height="21" viewBox="0 0 21 21" fill="none">
                        <circle cx="10.5" cy="10.5" r="10.5" fill="#FF6155"/>
                        <path d="M6 11.3812L8.73464 14L15 8" stroke="white" stroke-width="2"/>
                        </svg>
                        <span>Measuring to ensure updates are a success</span>
                    </li>
                    <li><svg xmlns="http://www.w3.org/2000/svg" width="21" height="21" viewBox="0 0 21 21" fill="none">
                        <circle cx="10.5" cy="10.5" r="10.5" fill="#FF6155"/>
                        <path d="M6 11.3812L8.73464 14L15 8" stroke="white" stroke-width="2"/>
                        </svg>
                        <span>And much more!</span>
                    </li>
                </ul>
            </div>
            <form on:submit|preventDefault={handleSubmit}>
                    <div class="email-label">
                      <label for="email">Email address</label>
                      <span id="error" class:show-error={!emailIsValid}>Valid email required</span>  
                    </div>
                    <input id="email" name="email" type="email" class:show-error={!emailIsValid} placeholder="email@company.com" required>
                    <button class="btn subscribe" type="submit">Subscribe to monthly newsletter</button>
            </form>
        </div>
        <picture class="newsletter-logo">
            <source srcset="/illustration-sign-up-desktop.svg" media="(min-width: 768px)">
            <source srcset="/illustration-sign-up-mobile.svg" media="(max-width: 767px)">
            <img src="/illustration-sign-up-desktop.svg" alt="newsletter logo" role="presentation">
        </picture>
    </div>
  {:else}
    <div class="success">
      <div class="success-message">
        <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 21 21" fill="none">
          <circle cx="10.5" cy="10.5" r="10.5" fill="#FF6155"/>
          <path d="M6 11.3812L8.73464 14L15 8" stroke="white" stroke-width="1"/>
          </svg>
          <h1>Thanks for subscribing!</h1>
          <p>
            A confirmation email has been sent to <strong>{email}</strong>. 
            Please open it and click the button inside to confirm your subscription.
          </p>
      </div>
      <button class="btn" on:click={() => (submitted = false)}>Dismiss message</button>
    </div>
  {/if}