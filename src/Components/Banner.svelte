<script>
    import { onMount } from 'svelte';
  
    let banner = null;
  
    onMount(async () => {
      const res = await fetch('/api/banner');
      banner = await res.json();
    });
  </script>
  
  
  {#if banner}
    <section class="banner">
      <div class="banner-content">
        <h1>{banner.heading}</h1>
        <p>{banner.description}</p>
        <a href={banner.buttonLink} class="banner-button">
          {banner.buttonText}
        </a>
        <div class="rating">⭐️ {banner.rating} / 5</div>
      </div>
  
      <div class="banner-images">
        {#each banner.images as img}
          <img src={img.asset.url} alt="Banner Image" />
        {/each}
      </div>
    </section>
  {/if}
  
  <style>
    .banner {
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
      padding: 2rem;
      background: #fafafa;
    }
  
    .banner-content {
      max-width: 600px;
      margin-bottom: 2rem;
    }
  
    .banner-button {
      background: #f96332;
      color: #fff;
      padding: 0.75rem 1.5rem;
      border-radius: 5px;
      text-decoration: none;
      font-weight: bold;
      display: inline-block;
      margin-top: 1rem;
    }
  
    .rating {
      margin-top: 1rem;
      font-size: 1.1rem;
      color: #444;
    }
  
    .banner-images img {
      max-width: 300px;
      width: 100%;
      height: auto;
      margin: 0 auto;
    }
  
    @media (min-width: 768px) {
      .banner {
        flex-direction: row;
        justify-content: space-between;
        text-align: left;
      }
  
      .banner-content {
        max-width: 50%;
      }
  
      .banner-images {
        max-width: 40%;
      }
    }
  </style>
  