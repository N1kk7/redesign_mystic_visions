<template>
  <div class="footer">
    <div class="container">
      <div class="footer_content">
        <div class="footer_content_top">

          <div class="main">
            <div class="logo">
              LOGO
            </div>
            <div class="name">
              The Pillars of Wisdom
            </div>
          </div>

       
          <div class="list">
            <div class="list_title">
              Products
            </div>

            <ul>
              <li>
                Paperback & Hardcover
              </li>
              <li>
                Ships Worldwide
              </li>
              <li>
                Secure Checkout
              </li>
            </ul>

            
          </div>
          <div class="list">
            <div class="list_title">
              Services
            </div>

            <ul>
              <li>
                <NuxtLink to="/">Return policy</NuxtLink>
              </li>
              <li>
                Contact us
              </li>
            </ul>
          </div>

             <div class="list">
            <div class="list_title">
              Links
            </div>

            <ul>
              <li>
                Reviews
              </li>
              <li>
                Our book
              </li>

            </ul>

          </div>

        </div>
        <div class="footer_content_bottom">

          <!-- <div class="contact">
            <div class="contact">Contact us</div>
            <div class="icon">

            </div>
          </div> -->

          <div class="links">
            <div class="link">

            </div>
            <div class="link">

            </div>
            <div class="link">

            </div>
            <div class="link">

            </div>
            <div class="link">

            </div>
          </div>

          <div class="text">
            A framework for evaluating environments and tradeoffs.
          </div>
          <div class="final">
            2026 Mystic Visions LLC
          </div>

        </div>
      </div>
      <!-- <div class="footer_content">
        <div class="footer_content_top">
          <strong> The Pillars of Wisdom </strong>

          <div class="email_contact"></div>
        </div>

        <div class="footer_content_bottom">
          <div class="left_content">
            <div>© 2026 Mystic Visions LLC</div>
            <div>A framework for evaluating environments and tradeoffs.</div>
          </div>
          <div class="right_content">
            <ul>
              <li>Paperback & Hardcover</li>
              <li>Ships Worldwide</li>
              <li>Secure Checkout</li>
            </ul>

            <ul>
              <li>Terms</li>
              <li>Contact</li>
            </ul>
          </div>
        </div>
      </div> -->
    </div>
  </div>
</template>

<script setup></script>

<style scoped lang="scss">
.footer {
  width: 100%;
  height: auto;
  padding: 96px 0 40px;
  position: relative;
  background: #111318;
  color: white;

  &_content {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    justify-content: center;


    &_top {
      display: grid;
      grid-template-columns: 2fr 1fr 1fr 1fr;
      border-bottom: 1px solid rgba(255, 255, 255, 0.1);
      padding-bottom: 30px;

      // .list {
      //   display: flex;
      //   flex-direction: column;
      //   justify-content: flex-start;
      //   align-items: center;
      // }

      .main {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: flex-start;
        // gap: 10px;
        .logo {
          font-size: 4rem;
          font-family: 'Roboto', sans-serif;
          font-weight: 700;
          font-style: normal;
          line-height: 150%;
        }
        .name {
          font-size: clamp(1.5rem, 2.5vw, 2rem);
          font-family: 'Roboto', sans-serif;
          font-weight: 500;
          font-style: normal;
          line-height: 150%;
        }
      }

      .list {
        margin: 0 auto;
        @media screen and (max-width: 768px) {
          margin: 0;
          border-top: 1px solid rgba(255, 255, 255, 0.1);
          width: 100%;
          padding-block: 20px;
        }
      }

      .list_title {
        font-family: 'Roboto', sans-serif;
        color: rgb(253, 130, 43);
        font-size: 1.25rem;
        font-weight: 700;
        font-style: normal;
        line-height: 150%;
        margin-bottom: 20px;
      }


      ul {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: flex-start;
        gap: 8px;

        li{
          cursor: pointer;
          font-family: 'Roboto', sans-serif;
          font-size: 1.15rem;
          font-weight: 400;
        }

      }

      @media screen and (max-width: 768px) {
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      align-items: flex-start;
      gap: 30px;
      
    }

    }

    &_bottom {
      display: flex;
      flex-direction: column;
      justify-content: flex-start;
      align-items: center;
      padding-block: 25px;
      gap: 20px;

      .links {
        display: flex;
        justify-content: center;
        align-items: center;
        gap: 15px;


        .link {
          background: lightgrey;
          width: 25px;
          height: 25px;
          border-radius: 50%;
          display: flex;
          justify-content: center;
          align-items: center;
          cursor: pointer;
        }
      }

    }

    
  }

}
</style>
