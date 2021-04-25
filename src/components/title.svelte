<script>
  export let dataDate;
  export let title;

  import moment from 'moment';
  let timestamp = moment(dataDate).format('MMMM Do YYYY, h:mm:ss a');
</script>

<div class="flex flex-col text-center items-center text-3xl">
    <div class='p-2 rounded-md text-white font-bold bg-green-600 md:w-full'>{title}</div>
    <div class="mt-4 mb-10">
      { timestamp }
    </div>
</div>