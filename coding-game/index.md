# Coding Game


<style>

.categories-card
{
  margin: 0 auto;
  margin-top: 3rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-direction: row;
  flex-wrap: wrap;
  line-height: 1.6rem;

  .card-item
  {
    font-size: .875rem;
    text-align: left;
    width: 45%;
    display: flex;
    align-items: flex-start;
    margin-top: 2rem;
    min-height: 10rem;
    padding: 0 2%;
    position: relative;

    .card-item-wrapper
    {
      width: 100%;
      overflow: hidden;

      .card-item-title
      {
        font-size: 1.2rem;
        font-weight: bold;
        display: inline-block;
        margin-top: 1rem;
        margin-bottom: .75rem;
      }

      span
      {
        float: right;
        padding-right: 1rem;
      }
    }
  }
}

.archive-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-sizing: border-box;
  margin: .25rem 0 .25rem 1.5rem;
}

.archive-item-link {
  min-width: 10%;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;

  &:hover {
    color: $global-link-hover-color;
    background-color: transparent;
  }

  [theme=dark] & {
    color: $global-link-color-dark;

    &:hover {
      color: $global-link-hover-color-dark;
    }
  }
}

</style>

<div class="categories-card">
  <div class="card-item">
    <div class="card-item-wrapper"><h3 class="card-item-title"><i class="far fa-folder fa-fw"></i>&nbsp;Easy</h3>
      <article class="archive-item"><a href="{{< relref "chuck-norris.md" >}}" class="archive-item-link">Chuck Norris</a></article>
      <article class="archive-item"><a href="{{< relref "defibrillators.md" >}}" class="archive-item-link">Defibrillators</a></article>
      <article class="archive-item"><a href="{{< relref "horse-racing_duals.md" >}}" class="archive-item-link">Horse Racing Duals</a></article>
      <article class="archive-item"><a href="{{< relref "mars-lander-ep1.md" >}}" class="archive-item-link">Mars Lander - Ep.1</a></article>
      <article class="archive-item"><a href="{{< relref "power-of-thor.md" >}}" class="archive-item-link">Power of Thor</a></article>
      <article class="archive-item"><a href="{{< relref "temperatures.md" >}}" class="archive-item-link">Temperatures</a></article>
      <article class="archive-item"><a href="{{< relref "the-descent.md" >}}" class="archive-item-link">The Descent</a></article>
    </div>
  </div>
  <div class="card-item">
    <div class="card-item-wrapper"><h3 class="card-item-title"><i class="far fa-folder fa-fw"></i>&nbsp;Moderate</h3>
      <article class="archive-item"><a href="{{< relref "mars-lander-ep2.md" >}}" class="archive-item-link">Mars Lander - Ep.2</a></article>
      <article class="archive-item"><a href="{{< relref "network-cabling.md" >}}" class="archive-item-link">Network Cabling</a></article>
      <article class="archive-item"><a href="{{< relref "shadows-of-the-knight-ep1.md" >}}" class="archive-item-link">Shadows of the Knight</a></article>
    </div>
  
</div>
