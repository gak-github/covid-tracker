<script>
  export let dataDate;
  export let title;

  import moment from 'moment';
  let timestamp = moment(dataDate).format('MMMM Do YYYY, h:mm:ss a');
</script>

<div class="text-center">
    <h2 class="text-3xl font-bold">{title}</h2>
    <div class="text-3xl mt-4 mb-10">
      { timestamp }
    </div>
</div>