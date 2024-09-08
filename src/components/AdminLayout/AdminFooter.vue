<template>
    <footer id="footer" class="footer">
      <div class="copyright">
        &copy; Copyright <strong><span>NiceAdmin</span></strong>. All Rights Reserved
      </div>
      <div class="credits">
        Designed by <a href="https://bootstrapmade.com/">BootstrapMade</a>
      </div>
    </footer><!-- End Footer -->
  
    <a href="#" class="back-to-top d-flex align-items-center justify-content-center"><i class="bi bi-arrow-up-short"></i></a>
  </template>
  
  <script>
  export default {
    name: 'AdminFooter',
    mounted() {
 
      this.loadScript('assets/vendor/apexcharts/apexcharts.min.js');
      this.loadScript('assets/vendor/bootstrap/js/bootstrap.bundle.min.js');
      this.loadScript('assets/vendor/chart.js/chart.umd.js');
      this.loadScript('assets/vendor/echarts/echarts.min.js');
      this.loadScript('assets/vendor/quill/quill.js');
      this.loadScript('assets/vendor/simple-datatables/simple-datatables.js');
      this.loadScript('assets/vendor/tinymce/tinymce.min.js');
      this.loadScript('assets/vendor/php-email-form/validate.js');
      this.loadScript('assets/js/main.js');
    },
    methods: {
      loadScript(src) {
        const script = document.createElement('script');
        script.src = src;
        script.async = true;
        document.body.appendChild(script);
      }
    }
  };
  </script>
  
  <style scoped>

  </style>
  