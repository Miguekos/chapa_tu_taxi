<template>
  <q-page>
    <div class="row">
      <div class="col-md-3"></div>
      <div class="col-xs-12 col-md-6">
        <div class="text-center">
          <q-img src="logo.png"></q-img>
        </div>
        <q-list>
          <q-form @submit="onSubmit">
            <q-item class="text-justify">
              <q-item-section>
                Aprovecha esta oportunidad, ten tu mototaxi propia y empieza a
                emprender 🛺 😎 Registra tus datos de contacto aquí para que
                nuestros asesores puedan pre evaluarte Pre evaluación 100%
                digital 👩🏽‍💻 Si tienes alguna duda, escríbenos por inbox en
                nuestra página en Facebook. Encuéntranos como REINVENTING.
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <q-input
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  v-model="apellido_paterno"
                  ref="apellido_paterno"
                  label="Apellido Paterno"
                ></q-input>
              </q-item-section>
              <q-item-section>
                <q-input
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  v-model="apellido_materno"
                  ref="apellido_materno"
                  label="Apellido Materno"
                ></q-input>
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <q-input
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  v-model="nombres"
                  ref="nombres"
                  label="Nombres"
                ></q-input>
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <q-input
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length === 8) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  counter
                  maxlength="8"
                  v-model="numero_dni"
                  ref="numero_dni"
                  label="Número de DNI *"
                ></q-input>
              </q-item-section>
              <q-item-section>
                <q-input
                  stack-label
                  outlined
                  label="Fecha de Nacimiento"
                  dense
                  v-model="fecha_nacimiento"
                  mask="date"
                  :rules="['date']"
                >
                  <template v-slot:append>
                    <q-icon name="event" class="cursor-pointer">
                      <q-popup-proxy
                        ref="qDateProxy"
                        transition-show="scale"
                        transition-hide="scale"
                      >
                        <q-date default-view="Years" v-model="fecha_nacimiento">
                          <div class="row items-center justify-end">
                            <q-btn
                              v-close-popup
                              label="Close"
                              color="primary"
                              flat
                            />
                          </div>
                        </q-date>
                      </q-popup-proxy>
                    </q-icon>
                  </template>
                </q-input>
                <!--                <q-input-->
                <!--                  outlined-->
                <!--                  lazy-rules-->
                <!--                  :rules="[-->
                <!--                    val => (val && val.length > 0) || 'Campo obligatorio'-->
                <!--                  ]"-->
                <!--                  stack-label-->
                <!--                  dense-->
                <!--                  v-model="fecha_nacimiento"-->
                <!--                  ref="fecha_nacimiento"-->
                <!--                  label="Fecha de nacimiento *"-->
                <!--                ></q-input>-->
              </q-item-section>
              <q-item-section>
                <q-input
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length === 9) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  counter
                  maxlength="9"
                  v-model="celular"
                  ref="celular"
                  label="Celular *"
                ></q-input>
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <q-input
                  outlined
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                  stack-label
                  dense
                  v-model="brevete"
                  ref="brevete"
                  label="¿Qué tipo de brevete para moto tienes? *"
                ></q-input>
              </q-item-section>
            </q-item>
            <!-- <q-item class="text-center">
                        <q-item-section>
                            <q-input outlined  stack-label dense v-model="model" ref="model" label="Celular *"></q-input>
                        </q-item-section>
                    </q-item> -->
            <!-- {{get_depart}} -->
            <q-item class="text-center">
              <q-item-section>
                <q-select
                  ref="region"
                  outlined
                  stack-label
                  dense
                  @input="getProv"
                  v-model="region"
                  :options="get_depart.result"
                  option-label="name"
                  option-value="id"
                  emit-value
                  map-options
                  label="Región:"
                  clearable
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                />
                <!-- <q-select outlined  stack-label dense v-model="model" ref="model" label="¿En qué distrito vives? *"></q-select> -->
              </q-item-section>
              <q-item-section>
                <q-select
                  ref="ciudad"
                  dense
                  outlined
                  stack-label
                  @input="getDistri"
                  v-model="ciudad"
                  :options="get_provin.result"
                  option-value="id"
                  option-label="name"
                  emit-value
                  map-options
                  label="Ciudad:"
                  clearable
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                />
              </q-item-section>
              <q-item-section>
                <q-select
                  ref="distrito"
                  dense
                  outlined
                  stack-label
                  v-model="distrito"
                  :options="get_distridistri.result"
                  option-value="id"
                  option-label="name"
                  emit-value
                  map-options
                  label="Distrito:"
                  clearable
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                />
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <q-input
                  outlined
                  stack-label
                  dense
                  autogrow
                  v-model="model"
                  ref="model"
                  label="¿Cuánta experiencia tienes como mototaxista? *"
                  lazy-rules
                  :rules="[
                    val => (val && val.length > 0) || 'Campo obligatorio'
                  ]"
                ></q-input>
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <q-item-section>
                <!--                <q-input-->
                <!--                  outlined-->
                <!--                  stack-label-->
                <!--                  dense-->
                <!--                  v-model="model"-->
                <!--                  ref="model"-->
                <!--                  label="Acepta usted la Política de Tratamiento de datos personales establecida por Reinventing en el siguiente enlace: https://bit.ly/2CvON7Q *"-->
                <!--                >-->
                <!--                </q-input>-->
                <q-toggle
                  style="align-self: center;"
                  v-model="accept"
                  label="Acepta usted la Política de Tratamiento de datos personales https://bit.ly/2CvON7Q *"
                />
              </q-item-section>
            </q-item>
            <q-item class="text-center">
              <!--              <q-item-section>-->
              <!--                <q-btn outline color="red" label="Cancelar"></q-btn>-->
              <!--              </q-item-section>-->
              <q-item-section>
                <q-btn
                  outline
                  color="green"
                  type="submit"
                  label="Enviar"
                  :loading="loadboton"
                ></q-btn>
              </q-item-section>
            </q-item>
          </q-form>
        </q-list>
      </div>
      <div class="col-md-3"></div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      loadboton: false,
      accept: false,
      submitResult: [],
      get_depart: "",
      get_provin: "",
      get_distridistri: "",
      region: "",
      ciudad: "",
      distrito: "",
      model: "",
      apellido_paterno: "",
      apellido_materno: "",
      nombres: "",
      numero_dni: "",
      fecha_nacimiento: "",
      celular: "",
      brevete: ""
    };
  },
  methods: {
    async getProv() {
      const respon = await this.$axios.get(
        `https://api.apps.com.pe/sgsform/provin/${this.region}`
      );
      this.get_provin = respon.data;
      this.ciudad = "";
      this.distrito = "";
    },
    async getDistri() {
      const respon = await this.$axios.get(
        `https://api.apps.com.pe/sgsform/distri/${this.ciudad}`
      );
      this.get_distridistri = respon.data;
      this.distrito = "";
    },
    async onSubmit() {
      try {
        this.loadboton = true;
        if (this.accept) {
          const JsonEnviar = {
            get_depart: this.get_depart,
            get_provin: this.get_provin,
            get_distridistri: this.get_distridistri,
            region: this.region,
            ciudad: this.ciudad,
            distrito: this.distrito,
            model: this.model,
            apellido_paterno: this.apellido_paterno,
            apellido_materno: this.apellido_materno,
            nombres: this.nombres,
            numero_dni: this.numero_dni,
            fecha_nacimiento: this.fecha_nacimiento,
            celular: this.celular,
            brevete: this.brevete
          };
          console.log(JsonEnviar);
          this.$q.notify({
            position: "top-right",
            message: "Registro Correcto",
            color: "green"
          });
          this.loadboton = false;
        } else {
          this.$q.notify({
            position: "top-right",
            message: "Debe aceptar los terminos y condiciones",
            color: "red"
          });
          this.loadboton = false;
          this.$router.push("/");
        }
      } catch (e) {
        console.log(e);
        this.$q.notify({
          position: "top-right",
          message: "Oh oh..!! Comicate con nosotros algo salio mal",
          color: "red"
        });
        this.loadboton = false;
      }
    },
    paso(val) {
      if (val === 3) {
        this.$refs.nombres.validate();
        this.$refs.apellidos.validate();
        this.$refs.tipodocumento.validate();
        this.$refs.documentIdentidad.validate();
        this.$refs.fechaNacimiento.validate();
        this.$refs.correoElectronico.validate();
        this.$refs.teleCelular.validate();
        this.$refs.pais.validate();
        this.$refs.region.validate();
        this.$refs.ciudad.validate();
        this.$refs.distrito.validate();
        this.$refs.direccion.validate();
        this.$refs.enterarte.validate();
        if (
          this.$refs.nombres.hasError ||
          this.$refs.apellidos.hasError ||
          this.$refs.tipodocumento.hasError ||
          this.$refs.documentIdentidad.hasError ||
          this.$refs.fechaNacimiento.hasError ||
          this.$refs.correoElectronico.hasError ||
          this.$refs.teleCelular.hasError ||
          this.$refs.pais.hasError ||
          this.$refs.region.hasError ||
          this.$refs.ciudad.hasError ||
          this.$refs.distrito.hasError ||
          this.$refs.direccion.hasError ||
          this.$refs.enterarte.hasError
        ) {
          this.formHasError = true;
          return false;
        } else {
          // this.$q.notify({
          //   icon: "done",
          //   color: "positive",
          //   message: "Submitted"
          // });
          return true;
        }
      } else if (val === 4) {
        this.$refs.Industriaogiro.validate();
        this.$refs.areadondetrabaja.validate();
        this.$refs.Cargoopuesto.validate();
        this.$refs.Centrodetrabajo.validate();
        return !(
          this.$refs.Industriaogiro.hasError ||
          this.$refs.areadondetrabaja.hasError ||
          this.$refs.Cargoopuesto.hasError ||
          this.$refs.Centrodetrabajo.hasError
        );
      } else {
        return true;
      }
    }
  },
  async created() {
    const respon = await this.$axios.get(
      `https://api.apps.com.pe/sgsform/depart`
    );
    this.get_depart = respon.data;
  }
};
</script>
<style>
.q-item {
  min-height: 48px;
  padding: 2px 16px !important;
  color: inherit;
  transition: color 0.3s, background-color 0.3s;
}
</style>
