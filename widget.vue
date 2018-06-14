          <!-- Intuitive Cron format input -->
          <label> Reportes Programados </label>
          <md-button-toggle md-single>
            <md-tooltip md-direction="bottom">Los reportes se pueden enviar periodicamente (cada cierto tiempo cada ciertos dias) o a una hora fija cada ciertos dias.</md-tooltip>
            <md-button v-on:click='cron_type="periodically"' v-bind:class='{"md-toggle": cron_type == "periodically"}'> <md-icon>publish</md-icon> Periodicamente </md-button>
            <!-- <md-button v-on:click='cron_type="timeFrame"' v-bind:class='{"md-toggle": cron_type == "timeFrame"}'> <md-icon>publish</md-icon> Periodicamente en un rango de tiempo</md-button> -->
            <md-button v-on:click='cron_type="fixedTime"' v-bind:class='{"md-toggle": cron_type == "fixedTime"}'> <md-icon>publish</md-icon> Hora fija recurrente </md-button>
          </md-button-toggle>

          <div v-if="cron_type==='periodically'">
            <md-button-toggle md-single>
              <md-button v-on:click='periodicity="minutes"' v-bind:class='{"md-toggle": periodicity == "minutes"}'> Minutos </md-button>
              <md-button v-on:click='periodicity="hours"' v-bind:class='{"md-toggle": periodicity == "hours"}'> Horas </md-button>
            </md-button-toggle>

            <md-input-container>
              <md-tooltip md-direction="bottom">Cada cuantos minutos será enviado el reporte.</md-tooltip>
              <label v-if="periodicity=='minutes'">¿Cada cuantos minutos?</label>
              <label v-if="periodicity=='hours'">¿Cada cuantas horas?</label>
              <md-input v-if="periodicity=='minutes'" numeric v-model='every_x_minutes'></md-input>
              <md-input v-if="periodicity=='hours'" numeric v-model='every_x_hours'></md-input>
            </md-input-container>  

            <md-button-toggle md-single>
              <md-button v-on:click='day_type="week_days"' v-bind:class='{"md-toggle": day_type == "week_days"}'> Días de la semana </md-button>
              <md-button v-on:click='day_type="month_days"' v-bind:class='{"md-toggle": day_type == "month_days"}'> Días del mes </md-button>
            </md-button-toggle>

            <md-input-container v-if="day_type=='week_days'">
              <md-tooltip md-direction="bottom">Día en que será enviado el reporte. Deje en blanco para que sea ninguno</md-tooltip>
              <label >¿Qué día de la semana?</label>
                <md-select v-model="week_day" placeholder="Día de la semana">
                  <md-option value='1'>Lunes</md-option>
                  <md-option value='2'>Martes</md-option>
                  <md-option value='3'>Miércoles</md-option>
                  <md-option value='4'>Jueves</md-option>
                  <md-option value='5'>Viernes</md-option>
                  <md-option value='6'>Sábado</md-option>
                  <md-option value='7'>Domingo</md-option>
                  <md-option value="*">Todos los días</md-option>
                </md-select>
            </md-input-container>  

            <md-input-container v-if="day_type=='month_days'">
              <md-tooltip md-direction="bottom">Día en que será enviado el reporte.</md-tooltip>
              <label >¿Qué día del mes?</label>
              <md-input numeric v-model='month_day'></md-input>
            </md-input-container>  
          </div>

          <div v-else>
            <md-input-container>
              <md-tooltip md-direction="bottom">Hora a la que el reporte será enviado en los días deseados</md-tooltip>
              <label >¿A qué hora?</label>
                <md-select v-model="recurrent_fixed_time" placeholder="Hora del día">
                  <md-option value='0'>Media noche</md-option>
                  <md-option value='1'>1:00 AM</md-option>
                  <md-option value='2'>2:00 AM</md-option>
                  <md-option value='3'>3:00 AM</md-option>
                  <md-option value='4'>4:00 AM</md-option>
                  <md-option value='5'>5:00 AM</md-option>
                  <md-option value='6'>6:00 AM</md-option>
                  <md-option value="7">7:00 AM</md-option>
                  <md-option value="8">8:00 AM</md-option>
                  <md-option value="9">9:00 AM</md-option>
                  <md-option value="10">10:00 AM</md-option>
                  <md-option value="11">11:00 AM</md-option>
                  <md-option value="12">Medio día</md-option>
                  <md-option value="13">1:00 PM</md-option>
                  <md-option value="14">2:00 PM</md-option>
                  <md-option value="15">3:00 PM</md-option>
                  <md-option value="16">4:00 PM</md-option>
                  <md-option value="17">5:00 PM</md-option>
                  <md-option value="18">6:00 PM</md-option>
                  <md-option value="19">7:00 PM</md-option>
                  <md-option value="20">8:00 PM</md-option>
                  <md-option value="21">9:00 PM</md-option>
                  <md-option value="22">10:00 PM</md-option>
                  <md-option value="23">11:00 PM</md-option>
                </md-select>
            </md-input-container>  

            <md-button-toggle md-single>
              <md-button v-on:click='day_type="week_days"' v-bind:class='{"md-toggle": day_type == "week_days"}'> Días de la semana </md-button>
              <md-button v-on:click='day_type="month_days"' v-bind:class='{"md-toggle": day_type == "month_days"}'> Días del mes </md-button>
            </md-button-toggle>

            <md-input-container v-if="day_type=='week_days'">
              <md-tooltip md-direction="bottom">Día en que será enviado el reporte. Deje en blanco para que sea ninguno</md-tooltip>
              <label >¿Qué día de la semana?</label>
                <md-select v-model="week_day" placeholder="Día de la semana">
                  <md-option value='1'>Lunes</md-option>
                  <md-option value='2'>Martes</md-option>
                  <md-option value='3'>Miércoles</md-option>
                  <md-option value='4'>Jueves</md-option>
                  <md-option value='5'>Viernes</md-option>
                  <md-option value='6'>Sábado</md-option>
                  <md-option value='7'>Domingo</md-option>
                  <md-option value="*">Todos los días</md-option>
                </md-select>
            </md-input-container>  

            <md-input-container v-if="day_type=='month_days'">
              <md-tooltip md-direction="bottom">Día en que será enviado el reporte.</md-tooltip>
              <label >¿Qué día del mes?</label>
              <md-input numeric v-model='month_day'></md-input>
            </md-input-container>  
          </div>

          <!-- TODO: Add support for periodicity within a time frame -->
          <!-- <md-input-container v-if="cron_type==='timeFrame'">
            <md-tooltip md-direction="bottom">Código al cual el usuario debe enviar los mensajes destinados a esta campaña. Ex: 897680</md-tooltip>
            <label>Time Frame</label>
            <md-input v-model='campaign.short_code'></md-input>
          </md-input-container> -->
          
          <!-- Intuitive Cron format input -->

    generateCronExpression () {
      let vc = this

      if (vc.cron_type == 'periodically') {
        if (vc.periodicity == 'minutes') {
          if (vc.day_type == 'week_days') {
            vc.cron_expression = '*/' + vc.every_x_minutes + ' * * * ' + vc.week_day
          }else {
            vc.cron_expression = '*/' + vc.every_x_minutes + ' * ' + vc.month_day + ' * *'
          }
        } else {
          if (vc.day_type == 'week_days') {
            vc.cron_expression = '* ' + '*/' + vc.every_x_hours + ' * * ' + vc.week_day
          }else {
            vc.cron_expression = '*/' + vc.every_x_hours + '*/' + vc.every_x_hours + vc.month_day + ' * '
          }
        }
      }

      if (vc.cron_type == 'fixedTime') {
        if (vc.day_type == 'week_days') {
          vc.cron_expression = '0 ' + vc.recurrent_fixed_time + ' * * ' + vc.week_day
        } else {
          vc.cron_expression = '0 ' + vc.recurrent_fixed_time + ' ' + vc.month_day + ' *'
        }
      }

      vc.campaign.reports_schedule.push(vc.cron_expression)
      console.log('campaign-detail#generateCronExpression - ' + vc.cron_expression)
    },