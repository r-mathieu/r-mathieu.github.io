# Personal Project


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
    <div class="card-item-wrapper">
      <article class="archive-item"><a href="https://github.com/r-mathieu/E-Ink-Trainstation" class="archive-item-link">E-ink Trainstation</a></article>
      <a href="https://github.com/r-mathieu/E-Ink-Trainstation">{{<image src="https://raw.githubusercontent.com/r-mathieu/E-Ink-Trainstation/main/git-page/header.png">}}</a>
      <article class="archive-item">A new project is coming</article>
    </div>
</div>