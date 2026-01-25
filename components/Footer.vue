<template>
  <div class="footer">
    <div class="container">
      <div class="footer_content">
        <div class="footer_content_top">
          <div class="main">
            <div class="main_wrapper">
              <div class="logo">
                <NuxtImg
                  src="/images/header-logo.webp"
                  alt="logo"
                  width="150"
                  height="150"
                  priority
                />
              </div>
              <div class="name">The Pillars of Wisdom</div>
            </div>

            <div class="mobile_products">
              <div class="list">
                <div class="list_title">Products</div>

                <ul>
                  <li>Paperback & <br/> Hardcover</li>
                  <li>Ships Worldwide</li>
                  <li>Secure Checkout</li>
                </ul>
              </div>
            </div>
          </div>

          <div class="list desktop_list">
            <div class="list_title">Products</div>

            <ul>
              <li>Paperback &<br/> Hardcover</li>
              <li>Ships Worldwide</li>
              <li>Secure Checkout</li>
            </ul>
          </div>
          <div class="list desktop_list">
            <div class="list_title">Services</div>

            <ul>
              <li>
                <NuxtLink to="/">Return policy</NuxtLink>
              </li>
              <li>Contact us</li>
            </ul>
          </div>

          <div class="list desktop_list">
            <div class="list_title">Links</div>

            <ul>
              <li>Reviews</li>
              <li>Our book</li>
            </ul>
          </div>

          <div class="mobile_list_wrapper">
            <div class="list">
              <div class="list_title">Services</div>

              <ul>
                <li>
                  <NuxtLink to="/">Return policy</NuxtLink>
                </li>
                <li>Contact us</li>
              </ul>
            </div>

            <div class="list">
              <div class="list_title">Links</div>

              <ul>
                <li>Reviews</li>
                <li>Our book</li>
              </ul>
            </div>
          </div>
        </div>

        <div class="footer_content_bottom">

          <div class="text">
            A framework for evaluating environments and tradeoffs.
          </div>
          <div class="final">2026 Mystic Visions LLC</div>
        </div>
      </div>
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

      .main {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: flex-start;
        transform: translateY(-15%);
        gap: 20px;
        &_wrapper {
          display: flex;
            flex-direction: column;
            justify-content: flex-start;
            align-items: flex-start;
            gap: 35px;
          @media screen and (max-width: 480px) {
            align-items: center;
            margin: 0 auto;
            gap: 15px;

          }
        }
        .name {
          font-size: clamp(1.5rem, 2.5vw, 2rem);
          font-family: "Roboto", sans-serif;
          font-weight: 500;
          font-style: normal;
          line-height: 150%;
        }

        .mobile_products {
          display: none;


          @media screen and (max-width: 768px) {
            display: block;
            padding-right: 10px;

            .list {
            padding-block: 0;

            }
          }

          
        }

        @media screen and (max-width: 768px) {
          width: 100%;
          height: 100%;
          display: flex;
          align-items: flex-start;
          justify-content: space-between;
          transform: translateY(0);
          flex-direction: row;
        }

        @media screen and (max-width: 480px) {
            flex-direction: column;
            align-items: flex-start;
            gap: 10px;
          }
      }

      .list {
        margin: 0 auto;
        @media screen and (max-width: 768px) {
          margin: 0;
          width: 100%;
          padding-block: 20px;
          // display: none;
        }
        @media screen and (max-width: 480px) {
          padding-block: 0;
        }
      }

      .desktop_list {
        @media screen and (max-width: 768px) {
          display: none;
        }
      }

      .mobile_list_wrapper {
        display: none;

        @media screen and (max-width: 768px) {
          display: flex;
          flex-direction: row;
          justify-content: space-between;
          border-top: 1px solid rgba(255, 255, 255, 0.1);
          align-items: center;
          padding-top: 20px;
          width: 100%;
        }
      }

      .list_title {
        font-family: "Roboto", sans-serif;
        color: rgb(253, 130, 43);
        font-size: 1.5rem;
        font-weight: 700;
        font-style: normal;
        line-height: 150%;
        margin-bottom: 25px;

        @media screen and (max-width: 768px) {
          margin-bottom: 20px;
        }
      }

      ul {
        display: flex;
        flex-direction: column;
        justify-content: flex-start;
        align-items: flex-start;
        gap: 12px;

        li {
          cursor: pointer;
          font-family: "Roboto", sans-serif;
          font-size: 1.25rem;
          font-weight: 400;
          color: white;
          transition: all ease 0.3s;
          cursor: pointer;


          @media screen and (min-width: 1024px) {
            &:hover {
              color: rgb(240, 143, 74);
              transition: all ease 0.3s;

            }
          }
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


      .text, .final {
        text-align: center;
      }
    }
  }

  @media screen and (max-width: 768px) {
    padding: 75px 0 35px;
  }
  @media screen and (max-width: 480px) {
    padding: 50px 0 25px;
  }
}
</style>
