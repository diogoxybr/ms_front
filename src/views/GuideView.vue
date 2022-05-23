<template>
<div class="container mt-5">
    <h1 class="mb-5">Guia básico de cultivo</h1>
  <div class="accordion" role="tablist">
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-1 variant="info">Planejamento da horta</b-button>
      </b-card-header>
      <b-collapse id="accordion-1" accordion="my-accordion" role="tabpanel">
        <b-card-body>
            <b-embed
              type="iframe"
              aspect="16by9"
              src="https://www.youtube.com/embed/GUppN-HvaBk"
              allowfullscreen
            ></b-embed>
        </b-card-body>
      </b-collapse>
    </b-card>

  <div class="accordion" role="tablist">
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-2 variant="info">Cuidados com a horta</b-button>
      </b-card-header>
      <b-collapse id="accordion-2" accordion="my-accordion" role="tabpanel">
        <b-card-body>
            <b-embed
              type="iframe"
              aspect="16by9"
              src="https://www.youtube.com/embed/C3oDTh57rdI"
              allowfullscreen
            ></b-embed>
        </b-card-body>
      </b-collapse>
    </b-card>
  </div>

  <div class="accordion" role="tablist">
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-3 variant="info">Como fazer a colheita</b-button>
      </b-card-header>
      <b-collapse id="accordion-3" accordion="my-accordion" role="tabpanel">
        <b-card-body>
            <b-embed
              type="iframe"
              aspect="16by9"
              src="https://www.youtube.com/embed/bv1wLU31Wq0"
              allowfullscreen
            ></b-embed>
        </b-card-body>
      </b-collapse>
    </b-card>
  </div>

  <div class="accordion" role="tablist">
    <b-card no-body class="mb-1">
      <b-card-header header-tag="header" class="p-1" role="tab">
        <b-button block v-b-toggle.accordion-4 variant="info">Playlist completa de vídeos sobre horta !</b-button>
      </b-card-header>
      <b-collapse id="accordion-4" accordion="my-accordion" role="tabpanel">
        <b-card-body>
            <b-embed
              type="iframe"
              aspect="16by9"
              src="https://www.youtube.com/embed/playlist?list=PL0levlxBCArds38xhOaPRzDikaHEAoq9p"
              allowfullscreen
            ></b-embed>
        </b-card-body>
      </b-collapse>
    </b-card>
  </div>
</div>
</div>
</template>
